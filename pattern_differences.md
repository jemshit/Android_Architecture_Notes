#### Why use patterns?
> "Well one can certainly build software applications without using any of these patterns, but by using these patterns we can achieve *separation of concerns* design principle. These help in improving maintainability of the application. Another important reason why these patterns became popular is implementing these patterns improve the testability of the application using automated unit tests." [[2]](#3-references)


## 1. Overview

<p align="center"><img src="https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/presentation_patterns.png" width="512" height="289" alt="Presentation Patterns"/></p>

Figure Reference: [[2]](#3-references)


## 2. Differences

<p align="center"><img src="https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvc_mvp_mvvm.png" width="640" height="256" alt="MVC vs MVP vs MVVM"/></p>

Figure Reference: [[1]](#3-references)

#### a) MVC

"Let’s look at MVC first. You’ll notice a few things about the diagram:

- The input is directed at the Controller first, not the view. That input might be coming from a user interacting with a page, but it could also be from simply entering a specific url into a browser. In either case, its a Controller that is interfaced with to kick off some functionality.

- There is a many-to-one relationship between the Controller and the View. That’s because a single controller may select different views to be rendered based on the operation being executed.

- Note the one way arrow from Controller to View. This is because the View doesn’t have any knowledge of or reference to the controller.

- The Controller does pass back the Model, so there is knowledge between the View and the expected Model being passed into it, but not the Controller serving it up.

- ... When you first try to access an MVC application, you would type something like this: 'www.somewebsite.com/customers'. When that request comes in, the MVC routing engine determines which controller "customers" refers to and directs it to the proper or default method. Its within that method where its determined what view should be rendered. Let's say you clicked a link on the rendered view to 'www.somewebsite.com/customerlist'. Same thing happens - the routing engine determines which controller "customerlist" is referring to and that controller determines which view gets rendered. That's one of the biggest diferences between MVC and traditional ASP.NET webform apps - you're not navigating to the location of a page in a folder structure, you're passing a request to a controller that determines what gets rendered...  The view knows information about what model its being passed for binding purposes. However, the **view doesn't know how to get the model or what context the model is in as far as state**. It only knows that it can expect a Customer object, for example, and it has helpers to bind properties of the customer to itself." [[1]](#3-references)

- "**In the MVC, the Controller is responsible for determining which View to display in response to any action** including when the application loads. *This differs from MVP where actions route through the View to the Presenter.* **In MVC, every action in the View correlates with a call to a Controller along with an action.** In the web each action involves a call to a URL on the other side of which there is a Controller who responds. Once that Controller has completed its processing, it will return the correct View. The sequence continues in that manner throughout the life of the application:  
Action in the View  -> Call to Controller  -> Controller Logic -> Controller returns the View.  
One other big difference about MVC is that the View does not directly bind to the Model. **The view simply renders, and is completely stateless.** *In implementations of MVC the View usually will not have any logic in the code behind. This is contrary to MVP where it is absolutely necessary because, if the View does not delegate to the Presenter, it will never get called.*" [[3]](#3-references)

- "...**in MVC, controller methods are based on behaviors** -- in other words, *you can map multiple views (but same behavior) to a single controller.* **In MVP, the presenter is coupled closer to the view, and usually results in a mapping that is closer to one-to-one,** i.e. a view action maps to its corresponding presenter's method. You typically wouldn't map another view's actions to another presenter's (from another view) method." [[4]](#3-references)

#### b) MVP

"Now let’s look at the MVP pattern. It looks very similar to MVC, except for some key distinctions:

- The input begins with the View, not the Presenter.

- There is a one-to-one mapping between the View and the associated Presenter.

- The View holds a reference to the Presenter. The Presenter is also reacting to events being triggered from the View, so its aware of the View its associated with.

- The Presenter updates the View based on the requested actions it performs on the Model, but the View is not Model aware." [[1]](#3-references)

- “The first element of Potel is to treat the view as a structure of widgets, widgets that correspond to the controls of the Forms and Controls model and *remove any view/controller separation*. **The view of MVP is a structure of these widgets. It doesn't contain any behavior that describes how the widgets react to user interaction.** *The active reaction to user acts lives in a separate presenter object. The fundamental handlers for user gestures still exist in the widgets, but these handlers merely pass control to the presenter*. The presenter then decides how to react to the event…” [[6]](#3-references)

- "MVP uses a Supervising Controller (a presenter when view is dumb) to manipulate the model. **Widgets hand off user gestures** to the Supervising Controller. *Widgets aren't separated into views and controllers.* You can think of presenters as being like controllers but without the initial handling of the user gesture. However it's also important to note that presenters are typically at the form level, rather than the widget level - this is perhaps an even bigger difference." [[6]](#3-references)

- "...Furthermore the presenter is welcome to directly access widgets for behaviors that don't fit into the Observer Synchronization." [[6]](#3-references)

- "From our point of view *MVP is not a variant or enhancement* *of MVC* because that would mean that the Controller gets replaced by the Presenter. In our opinion **MVP wraps around MVC**. Take a look at your MVC powered app. The Presenter sits in the middle between controller and model like this:" [[5]](#3-references)

<p align="center"><img src="https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvc_vs_mvp.png" width="446" height="357" alt="MVP vs MVC"/></p>

Figure reference: [[5]](#3-references)

- "In our opinion the *Presenter does not replace the Controller*. Rather the Presenter coordinates or supervises **the View which the Controller is part of**. The Controller is the component that handles the click events and calls the corresponding Presenter methods. The Controller is the responsible component to control animations like hiding ProgressBar and displaying ListView instead. The Controller is listening for scroll events on the ListView i.e. to do some parallax item animations or scroll the toolbar in and out while scrolling the ListView. **So all that UI related stuff still gets controlled by a
Controller and not by a Presenter** (i.e. *Presenter should not be an OnClickListener*). The Presenter is responsible to **coordinate the overall state** of the view layer (composed of UI widgets and Controller). So it's the job of the Presenter to tell the view layer
that the loading animation should be displayed now or that the ListView should be displayed because the data is ready to be displayed" [[5]](#3-references).

#### c) MVVM

"So with the MVC and MVP patterns in front of us, let’s look at the MVVM pattern and see what differences it holds:

- The input begins with the View, not the View Model.

- While the View holds a reference to the View Model, the View Model has no information about the View. This is why its possible to have a one-to-many mapping between various Views and one View Model…even across technologies. For example, a WPF View and a Silverlight View *could* share the same View Model. However, my own feeling is that this is a bad practice and creates Franken-ViewModels that have too many responsibilities. It’s better to keep it as a one-to-one mapping instead.

- You’ll also notice that the View has no idea about the Model in the MVVM pattern. This is because, as far as the View knows, its “Model” IS the View Model (hence its name). Because of how data-binding and other features like commanding work in WPF and Silverlight, there is rich communication between the View and View Model, isolating the View from having to know anything about what’s really happening behind the scenes." [[1]](#3-references)

- "..ViewModel only provides the data, whereas the View is responsible for consuming them." [[7]](#references)

#### d) PM
Presentation Model definition: https://martinfowler.com/eaaDev/PresentationModel.html

## 3. References

[1] "MVVM Compared To MVC and MVP," 21 11 2009. [Online]. Available: https://web.archive.org/web/20170829105757/http://geekswithblogs.net/dlussier/archive/2009/11/21/136454.aspx. [Accessed 03 03 2018].

[2] Manoj Jaggavarapu, "Presentation Patterns : MVC, MVP, PM, MVVM," 02 05 2012. [Online]. Available: https://manojjaggavarapu.wordpress.com/2012/05/02/presentation-patterns-mvc-mvp-pm-mvvm/. [Accessed 03 03 2018].

[3] "What are MVP and MVC and what is the difference?," [Online]. Available: https://stackoverflow.com/a/101561/3736955. [Accessed 03 03 2018].

[4] "What are MVP and MVC and what is the difference?," [Online]. Available: https://stackoverflow.com/questions/2056/what-are-mvp-and-mvc-and-what-is-the-difference#comment67878328_101561. [Accessed 03 03 2018].

[5] Hannes Dorfmann, "Model-View-Presenter," 25 05 2015. [Online]. Available: http://hannesdorfmann.com/mosby/mvp/. [Accessed 14 06 2017].

[6] Martin Fowler, "GUI Architectures," 18 07 2006. [Online]. Available: https://martinfowler.com/eaaDev/uiArchs.html. [Accessed 26 02 2018].

[7] Kamil Seweryn, "MVP to MVVM transformation" 20 01 2018. [Online]. Available: https://proandroiddev.com/mvp-to-mvvm-transformation-611959d5e0ca. [Accessed 21 10 2020].