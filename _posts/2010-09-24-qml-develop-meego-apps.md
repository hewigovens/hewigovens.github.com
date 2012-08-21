---
comments: true
date: 2010-09-24 20:51:12
layout: post
slug: qml-develop-meego-apps
title: 用QML开发MeeGo应用程序
wordpress_id: 61
categories:
- MeeGo
tags:
- meego
- qml
---

什么是[QML](http://doc.qt.nokia.com/4.7-snapshot/qdeclarativeintroduction.html)？




QML是一种描述应用程序UI的声明式语言，包括应用程序的外观（菜单、按钮、布局等）以及行为（点击事件）的描述。在QML中，UI界面被描述成一种树状的带属性对象的结构（类似于DOM）




[JavaScript](https://developer.mozilla.org/en/JavaScript)是QML中使用的脚本语言, 所以你最好是对它有一定程度了解再深入进行QML的学习（可以参考[JavaScript: The Definitive Guide](http://www.davidflanagan.com/javascript5/))。如果对HTML和CSS等Web技术有所理解是会有帮助的，但不是必需的。




上面是官方介绍的前两段，具体中文教程可以看看[Qt技术分享博客的系列教程](http://www.cuteqt.com/blog/?s=qml)，QML实际上是[Qt Quick](http://doc.qt.nokia.com/4.7-snapshot/qtquick.html)（Qt4.7.0中的新特性）核心组件之一：Qt Quick是一组旨在帮助开发者创建在移动电话，媒体播放器，机顶盒和其他便携设备上使用越来越多的直观、现代、流畅UI的工具集合。Qt Quick包括一组丰富的用户界面元素，一种用于描述用户界面的声明性语言（QML）及运行时，一组用于将这些高层次特性集成到经典的Qt应用程序的C++ API。




从官方的介绍可以看出，Qt Quick是为移动平台快速开发所量身打造的，先看一个实际例子：在MeeGo上运行的MeeNotes，除了业务逻辑，界面UI都是使用QML实现的




![](https://lh5.googleusercontent.com/MjsIJ3hE2ShXgMy7l8hAsxqTtXnNAtPjOUfuogxUpxdOGhtbh9MyFGwmHRI1DyFDdkN7TFdBvg7tmlhy8gntQHM7MSUw7_qzggWIVsCkG-6hmIGx1Q)




MeeNotes运行效果




![](https://lh4.googleusercontent.com/td4qP4XYL_g0CGEKHrxFhC7O7AdYPdqilTavmvm9Z4zddAXZngAPOxC9qlblD-6_9DgBdVvHDNE2AfPMh1Yo_o5EWCie4YWsMf5Lk4zJ_G4eWVtwvw)




横竖屏幕切换（点击那个星号～）




![](https://lh6.googleusercontent.com/TQ0IPh9Mm-UfRY12upue_JxXUMxXW5F0NRByS68wxmU1OrXaLNsW8RPWTLScKi4y7qSQZWS5qp5XGcXsV5UG-fwRJRW0vWGq3o984iIeI6jpmXHfPA)




在模拟器中运行效果




MeeNotes可以在[这里](http://qt.gitorious.org/qt-components)找到：使用git把qt-components和meenotes clone下来，然后先编译qt-components，这个依赖于qt4.7，是使用QML快速开发meego应用程序的关键，它实现了一套meego的QML Module，之后可以编译运行下MeeNotes，如果运行不了，请检查Qt安装目录里是否有 com.nokia.meego这个module（我的位于/usr/local/Trolltech/Qt-4.7.0/imports/com /meego）如果没有，则需要在qt-components解压目录下的 src/MeeGo 手动执行qmake/make/make install，进行编译安装。




简单看看MeeNotes下的实际代码




src目录下的**src.pro**，红色部分即是与使用libmeegotouch开发所不同之处 ：




TEMPLATE = app  

    
TARGET = ../MeeNotes 




LIBS += -lQtComponents  

      
HEADERS += models/meenotesmodel.h  




models/notemodel.h 




SOURCES += main.cpp  




models/meenotesmodel.cpp  




models/notemodel.cpp 




QT += declarative 





    
**再看主入口main.cpp：**




#include "models/meenotesmodel.h"  

    
#include <QApplication>




#include <QDeclarativeContext>  

      
#include <QDeclarativeComponent>




#include <QDir>




#include <QtComponents/qdeclarativewindow.h>




int main(int argc, char **argv) 




{ 




QApplication app(argc, argv);   
app.setApplicationName("MeeNotes"); 





    
//MeeNotesModel 是Model类




qmlRegisterType<NoteModel>();  

    
MeeNotesModel model; 




model.setSource("notes/"); 







//在哪查找main.qml




#ifndef MEENOTES_RESOURCE_DIR   
const QDir dir(QApplication::applicationDirPath()); 




const QUrl qmlPath(dir.absoluteFilePath("resource/default/main.qml")); 




#else   
const QDir dir(MEENOTES_RESOURCE_DIR);   
const QUrl qmlPath(dir.absoluteFilePath("main.qml")); 




#endif   
//创建能够解释qml运行的window




QDeclarativeWindow window(qmlPath); 




window.rootContext()->setContextProperty("meenotes", &model);   
window.window()->show();   
return app.exec(); 




} 





    
**查看main.qml：**




import Qt 4.7 




import com.meego 1.0  

      
Window { 




id: window 




Component.onCompleted: { 




window.nextPage(Qt.createComponent("NoteList.qml"))  

      
} 




} 





    
**查看NoteList.qml：  

      
**import Qt 4.7 




import com.meego 1.0 




Page { 




title: "MeeNotes"




actions: [ 




Action { 




iconId: "icon-m-toolbar-add" //新建note按钮的处理




onTriggered: { 




var note = meenotes.newNote(); 




note.title = (Math.random() > 0.5) ? "Cool title!" : ""; 




viewNote(note); 




} 




}, 




Action { 




iconId: "icon-m-toolbar-favorite-mark" //横竖屏切换的按钮处理  

      
onTriggered: { 




screen.orientation = screen.orientation == Screen.Portrait ? Screen.Landscape : Screen.Portrait; 




} 




} 




] 




Component {   
… … …//省略




}  

    
Rectangle { 




color: "white"




anchors.fill: parent 




} 




GridView { 




id: grid 




anchors.fill: parent 




model: meenotes 




cellWidth: 250 




cellHeight: 210 




delegate: noteDelegate 




} 




function viewNote(note) { 




window.nextPage(Qt.createComponent("Note.qml")); 




window.currentPage.note = note; 




} 




}




鉴于QML类似于web网页css的编写方式，效率已经很高了，但是似乎Qt Designer被我们忽视了，其实2.01版的Desinger已经可以使用meegotouch风格进行预览了，效果如下图：![](https://lh6.googleusercontent.com/5z7ZjbX8IQpupTJZFj3WOQikTjaD8fp_xPNP68w5R-3cipwLzvpTxbTeE2IQvQJhe1L3DgFurWJ0iExmDrYCXKm3bRYKOnmao8cNlEr7xxDzSid8Jw)




目前Designer并不能直接生成QML文件，下一个版本的Desinger以及在计划之中了，可以叫他Qt Quick Designer，在Qt Roadmap中已经可以体现出来了：




![](https://lh4.googleusercontent.com/nYL_bzp-N-RIFKleE9-g0pbghYo9xj2PvOmpgzdr8pyoSKMrQ2e4iXpOTyCgtfK3PAx34SdsIq5wuEF2EYey3a7F-Yy-J5lE1vfo4M8JeMIrYJdP_g)
