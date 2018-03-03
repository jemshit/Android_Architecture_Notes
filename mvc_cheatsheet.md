# MVC (Model-View-Controller)

Why use patterns ?
> "Well one can certainly build software applications without using any of these patterns, but by using these patterns we can achieve separation of concerns design principle. These help in improving maintainability of the application. Another important reason why these patterns became popular is implementing these patterns improve the testability of the application using automated unit tests." [[6]](#references)

## Original definition
Original paper link: http://heim.ifi.uio.no/~trygver/2007/MVC_Originals.pdf

"He originally defined Models, Views, and Controllers like this:
- **MODELS** – *Models represent knowledge.* A model could be a single object (rather uninteresting), or it could be some structure of objects.
- **VIEWS** — *A view is a (visual) representation of its model*. It would ordinarily highlight certain attributes of the model and suppress others. *It is thus acting as a presentation filter*.
- **CONTROLLERS** — *A controller is the link between a user and the system*. It provides the user with input by arranging for relevant views to present themselves in appropriate places on the screen. It provides means for user output by presenting the user with menus or other means of giving commands and data. The controller receives such user output, translates it into the appropriate messages and passes these messages on to one or more of the views." [[5]](#references)


## Original definition interpretation

#### by Stephen Walther

"In the context of a Graphical User Interface, the Model View Controller pattern was interpreted like this:

- **MODEL** – *A particular piece of data* represented by an application. For example, weather station temperature reading.
- **VIEW** – *One representation of data from the model.* **The same model might have multiple views associated with it.** For example, a temperature reading might be represented by both a label and a bar chart. The views are associated with a particular model through the Observer relationship.
- **CONTROLLER** – *Collects user input and modifies the model.* For example, the controller might collect mouse clicks and keystrokes and update the Model." [[5]](#references)

![MVC original diagram](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvc_original.png)

"Notice, in this figure, **that the View is updated indirectly from the Model.** When the Model changes, the Model raises an event, and the View changes in response to the event. Also, **notice that the Controller does not interact directly with the View.** Instead, the Controller modifies the Model, and since the View is observing the Model, the View gets updated. According to Martin Fowler, the primary benefit of this original version of the MVC pattern is *Separated Presentation* (which is described below)..." [[5]](#references)


#### by Martin Fowler
Lets start with data states before discussion:
- **Record state** (copy of data in database) [[1]](#references)
- **Session state** (in-memory record sets in application. “Essentially this provides a temporary local version of the data that the user works on until they save, or commit it, back to the database - at which point it merges with the record state.”) [[1]](#references)
- **Screen state** (inside the GUI components themselves) [[1]](#references)


Now lets check definition of **Data Binding** to understand one way of *synchronization between states of data* mentioned above:
- "A mechanism that ensures that any change made to the data in a *UI control (screen state)* is automatically carried over to the underlying *session state* (and vice versa)”. [[2]](#references)
- “Keeping screen state and session state synchronized is an important task. A tool that helped make this easier was Data Binding. The idea was that any change to either the control data, or the underlying record set was immediately propagated to the other. So if I alter the actual reading on the screen, the text field control effectively updates the correct column in the underlying record set." [[1]](#references)
-  "In general data binding gets tricky because if you have to avoid cycles where a change to the control, changes the record set, which updates the control, which updates the record set... The flow of usage helps avoid these - we load from the session state to the screen when the screen is opened, after that any changes to the screen state propagate back to the session state. It's unusual for the session state to be updated directly once the screen is up. As a result *data binding might not be entirely bi-directional* - just confined to initial upload and then propagating changes from the controls to the session state.” [[1]](#references)
- “Simple data edits are handled through data binding. **Complex changes are done in the form's event handling methods.**”  [[1]](#references) So if input data is just propagated, data binding is perfect solution. But if there is complex logic before propagating input data from user to domain layer, then you have to handle input event manually and send it to domain layer.

> **Controls** definiton: UI widget controls (text changed, button pressed…) ("The form observes the controls and has handler methods to react to interesting events raised by the controls.") [[1]](#references)


###### Interpretation

- “At the heart of MVC, and the idea that was the most influential to later frameworks, is what I call **Separated Presentation**. The idea behind Separated Presentation is to make a *clear division between domain objects that model our perception of the real world, and presentation objects that are the GUI elements we see on the screen*. **Domain objects should be completely self contained and work without reference to the presentation, they should also be able to support multiple presentations**, possibly simultaneously. This approach was also an important part of the Unix culture, and continues today allowing many applications to be manipulated through both a graphical and command-line interface." [[1]](#references)
- In MVC, the **domain element is referred to as the model**. *Model objects are completely ignorant of the UI…* In MVC I'm assuming a Domain Model of regular objects, rather than the Record Set notion that I had in Forms and Controls. This reflects the general assumption behind the design. Forms and Controls assumed that most people wanted to easily manipulate data from a relational database, MVC assumes we are manipulating regular... objects.” [[1]](#references)
- “… **The controller's job** is to take the user's input and figure out what to do with it.” [[1]](#references) But in web app, controller has urls that routes bla bla...
- “You'll notice that the text field controller didn't set the value in the view itself, it updated the model and then just let the observer mechanism take care of the updates. This is quite different to the forms and controls approach where the form updates the control and relies on data binding to update the underlying record-set. These two styles I describe as patterns: **Flow Synchronization** and **Observer Synchronization**. These two patterns describe alternative ways of handling the triggering of synchronization between *screen state* and *session state*. Forms and Controls do it through the flow of the application manipulating the various controls that need to be updated directly. **MVC does it by making updates on the model and then relying of the observer relationship to update the views that are observing that model…** The classic MVC example was a spreadsheet like screen of data with a couple of different graphs of that data in separate windows. The spreadsheet window didn't need to be aware of what other windows were open, *it just changed the model and Observer Synchronization took care of the rest…* While Observer Synchronization is nice it does have a downside... Observer behavior is hard to understand and debug because it's implicit behavior.” [[1]](#references)

> "**Flow Synchronization** is a very simple approach to explain. Essentially each time you do something that changes state that's shared across multiple screens, you tell each screen to update itself. The problem is that this means, in general, that every screen is somewhat coupled to the other the other screens in the application. If you have a lot of screens that are working in a very open-ended way, this can be nasty - which is Observer Synchronization is such a strong alternative." [[3]](#references)

> "**Observer Synchronization:** Synchronize multiple screens by having them all be observers to a shared area of domain data... Observer Synchronization uses a single area of domain oriented data and has each screen be an observer of that data. Any change in one screen propagates to that domain oriented data and thence to the other screens. This approach was a large part of the Model View Controller approach... Even the screen that makes the change doesn't need to refresh itself explicitly, since the observer mechanism will trigger the refresh in the same way as if another screen made the change." [[4]](#references)

- “The Presentation Model works well also for another presentation logic problem - **presentation state.** The basic MVC notion assumes that all the state of the view can be derived from the state of the model. In this case how do we figure out which station is selected in the list box? The **Presentation Model** solves this for us by giving us a place to put this kind of state. A similar problem occurs if we have save buttons that are only enabled if data has changed - again that's state about our interaction with the model, not the model itself.” [[1]](#references)


###### Soundbites on MVC:
-  **Separated Presentation**: Make a strong separation between presentation *(view & controller)* and domain *(model)* [[1]](#references)
- "**Divide GUI widgets into** a *controller* **(for reacting to user stimulus)** and *view* (for displaying the state of the model). **Controller and view should (mostly) not communicate directly but through the model.**" [[1]](#references)
- **Observer Synchronization**: Have views (and controllers) observe the model to allow multiple widgets to update without needed to communicate directly. [[1]](#references)


#### by Manoj Jaggavarapu
"In MVC pattern, model, view, controller triad exists for each object that can be manipulated by the user. Lets see what each of these does

- **Model :** Model means data, that is required to display in the view. It can sometimes be the exact data entities that are retrieved from the business layer or a variation of it. *Model encapsulates business tier.*

- **View :** *View is something that displays data to user.* In MVC pattern view should be simple and free of business logic implementation. *View invokes methods on Controller depending on user actions.* **In MVC pattern View monitors the model for any state change and displays updated model.** Model and View interact with each other using the Observer pattern.

- **Controller:** Controller is invoked by view, *it executes interacts with the model and performs actions that updates the model.* Controller doesn’t have an idea about the changes that it’s updates on the model resulted in the view. Often misunderstood in MVC pattern is the role of Controller. **It doesn’t mediate between the view and model,and its not responsible for updating the view. It simply process the user action and updates model,** its the view’s job to query and get the status of the changed model and render it.  **The only time Controller comes into picture is if a new view has to be rendered.**" [[6]](#references)


## Evolution

JavaServer Pages (JSP) had Model 2 method for creating application. In this method, "... the components of an MVC application work like this:
- MODEL – Business logic plus one or more data sources such as a relational database.
- VIEW – The user interface that displays information about the model to the user.
- CONTROLLER – The flow-control mechanism means by which the user interacts with the application...

**In this new version of the MVC model, there is no longer any relationship between the View and the Model. All communication between View and Model happens through the controller...** Several web application frameworks have adopted the Model 2 MVC pattern. In the Java world, these frameworks include Struts, Tapestry, and Spring. In the Ruby world, these frameworks include Ruby on Rails and Merb. In the Python world, these frameworks include Django. And, of course, in the ASP.NET world, these frameworks include ASP.NET MVC." [[5]](#references)

![MVC JSP diagram](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvc_jsp.png)

"In Model 2 pattern, **all web post requests go to front controller**, implemented as a http interceptor (http module in ASP.NET ),**which in turn figures out the appropriate controller depending on the structure of the incoming request URL** and services the request. The controller invokes a method that affects the model. The following diagram depicts the structure of Model2 pattern:"

![MVC Model2](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/model2_mvc.png)

"The main difference between classic MVC and Model2 is that **there is no direct contact between view and model. The Model in this pattern is not your typical business entities or Business layer, it’s more of a ViewModel** that captures the state of the view.  **The controller will be the one who will talk to BLL and update the model.  The interaction between the view and model is an indirect relationship.** Below sequence diagram depicts Model2 interactions using sequence diagram :"

![Model2 Sequence Diagram](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/model2_mvc_sequence.png)


#### MVC, Model 2, MVP, PM, MVVM
![MVC JSP diagram](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/presentation_patterns.png)
[[6]](#references)


## References

[1] Martin Fowler, "GUI Architectures," 18 07 2006. [Online]. Available: https://martinfowler.com/eaaDev/uiArchs.html. [Accessed 26 02 2018].

[2] Martin Fowler, "Data Binding," 25 05 2006. [Online]. Available: https://martinfowler.com/eaaDev/DataBinding.html. [Accessed 26 02 2018].

[3] Martin Fowler, "Flow Synchronization," 15 11 2004. [Online]. Available: https://martinfowler.com/eaaDev/FlowSynchronization.html. [Accessed 02 03 2018].
[2] Martin Fowler, "Data Binding," 25 05 2006. [Online]. Available: https://martinfowler.com/eaaDev/DataBinding.html. [Accessed 26 02 2018].

[4] Martin Fowler, "Observer Synchronization," 08 09 2004. [Online]. Available: https://martinfowler.com/eaaDev/MediatedSynchronization.html. [Accessed 02 03 2018].

[5] Stephen Walther, "The Evolution of MVC," 24 08 2008. [Online]. Available: http://stephenwalther.com/archive/2008/08/24/the-evolution-of-mvc. [Accessed 02 03 2018].
[4] Martin Fowler, "Observer Synchronization," 08 09 2004. [Online]. Available: https://martinfowler.com/eaaDev/MediatedSynchronization.html. [Accessed 02 03 2018].

[6] Manoj Jaggavarapu, "Presentation Patterns : MVC, MVP, PM, MVVM," 02 05 2012. [Online]. Available: https://manojjaggavarapu.wordpress.com/2012/05/02/presentation-patterns-mvc-mvp-pm-mvvm/. [Accessed 03 03 2018].

---
Last Edited: 03.03.2018
