---
layout: post
title: "Sense of good project structure"
description: What is a good project structure. How to implement it and make client happy?
category: work
tags: 
  - work
published: true
---

Once client asked me  - "Do you have a sense of a good project structure". I answered "Yes", as usual, but later 
start thinking about it....

When I started as Java programmer it was easy. Very well structured language, 2 books about code programming patterns,
simple use cases - MVC on client side, DAO on backend, Service layer, 3-4 most useful patterns like Adapter, Facede, Proxy etc and as much Injections as possible and stuff like that... Just put all patterns
 you know, make good folders architecture so everything Java requires for a good solution, good project.
 
 Later when I moved to games development with Java and AS3 I introduced some new and interesting patters - they called
 Game Development Patters - most of them were the same enterprise patterns but reworked or renamed for games development. Injections were so
 slow, some patterns because of needs in quick code...
 Here I used more Singletone, Commands, Mediators, MVC changed to MVP pattern and so on.
 
 
 It's interesting but .Net took MVVM pattern to development as the default pattern for WPF UI development.
 
 Last 2 or 3 years I was working on big multiplatform desktop applications, so can provide you some best practices I learned during the development.
 
 All project divide into 5 packages:
 - controller
 - model
 - service
 - utils
 - view
 
 Robotlegs was the only one base framework I used in all my projects. It supported Injections and configuration.
 I setup a config for every project:
 
         injector.map(ApplicationModel).asSingleton();
         injector.map(ProjectModel).asSingleton();
 
 
         mediatorMap.map(TimeLineView).toMediator(TimeLineMediator);
         mediatorMap.map(VideoPlayerView).toMediator(VideoPlayerMediator);
         
         commandMap.map(UndoAdvancedCommandEvent.NAME).toCommand(UndoAdvancedCommand);
          
          
 
 So global models were injected as singletones, every view had its own Midator and every command was executed with a command.
 Simple and powerful architecture.
 
 
 When view appears in display list Robotlegs creates a Mediator for it - the middle layer, which could control the View component and
 join it with base Event bus ( two way ).
 You can say it's like an MVP pattern, but no. Mediator in this case is just a support component and we still using MVC paradigm.
 
 
 When view model is ready Mediator passes it to View component and forget about it, View should take full responsible of MV interaction
 and pass some Controller related functionality to Mediator ( view View-to-Controller even bus ).
 
 
  
        addContextListener(ProjectLoadedEvent.NAME,onProjectLoaded);
        addViewListener(Event.CLOSING,onApplicationClosing);
        
        
            private function onProjectLoaded(event:ProjectLoadedEvent):void {
                view.setModel (event.data);
            }
            
            private function onProjectIntegrityHasProblems(event:ApplicationEvent):void {
                    dispatch (new ApplicationClosesEvent()); 
            }
            
            
            


As you can see Mediator just a manager for a View and connects it with application commands which do the most work in the app.


Code is easy to write, good decomposition, small command which contain all application logic, model-view bi directional binding ( React framework hello!!! )
And Im actually was very happy with thaT!!!


Unity. What to say about Unity... When you write code for Unity project you use mostly composition patterns instad of Inheritance. 
Very powerful patter and good fit for a Unity architecture. I spent 1 year working on different Unity projects. So same patters as before...
 Nothing new, nothing complicated... If you know how to program you just... program.....
 
 
Now Im starting with frontend... It blowing my mind... But actually I do the same things as before - think about better project structure, 
think about frameworks I could use in the application and then just put everything together and make a connections between components, 
write code and make everything working... Working good, working fast and look well....

Thank you....
