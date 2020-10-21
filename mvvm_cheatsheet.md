# MVVM (Model-View-ViewModel)

"Model/View/ViewModel is a variation of Model/View/Controller (MVC) that is tailored for modern UI development platforms
where the View is the responsibility of a designer rather than a classic developer.
The designer is generally a more graphical, artistic focused person, and does less classic coding than a traditional developer..
The design is almost always done in a declarative form like HTML or XAML.." [[8]](#references). 
"Just like its MVC predecessor, the View in MVVM can bind to the data and display updates, but without any coding at all,
just using XAML markup extensions. This way, the View is under the designer’s control, but can update its state from the
domain classes using the WPF binding mechanism. This fits the description of the Presentation Model pattern." [[9]](#references). 

![MVVM](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvvm.png)
[[1]](#references)

- "Model-View-ViewModel is an architectural approach used to **abstract the state and behaviour of a view**, which allows us to **separate the development of the UI from the business logic.**" [[2]](#references)
- "This is accomplished by the introduction of a ViewModel, whose responsibility is to expose the data objects of a model and handle any of the application logic involved in the display of a view." [[2]](#references)

## 1. Model

- "Data model containing business and validation logic" [[1]](#references) [[2]](#references)
- Does not contain any View reference or View related logic


## 2. View

- "Defines the structure, layout and appearance of a view on screen" [[2]](#references)
- "View in MVVM is similar to view in PM. It contains only the UI elements. The interaction between View and ViewModel happens using Data Binding, Commands and Notifications..." [[1]](#references)
- "..ViewModel only provides the data, whereas the View is responsible for consuming them." [[5]](#references)
- In Android, View can consume data using _LifecycleOwner_ and _LiveData_ classes, which stops observing (unsubscribes/disposes) the data at corresponding lifecycles automatically
- "Even if the View gets to decide how to handle data, that does not mean it needs to contain complicated logic. The idea is that ViewModel provides data in a form that View **simply takes and display** - no manipulation required." [[5]](#references)


## 3. ViewModel

- "Acts a link between the View and Model, dealing with any view logic" [[2]](#references)
- "ViewModel does not hold reference to the View" [[5]](#references)[[7]](#references)
- "View Model is equivalent to PresentationModel in PM pattern, it encapsulates presentation logic and data for the view.  ViewModel contains the state of the view and uses Commands, DataBinding and Notifications to communicate with the view." [[1]](#references)
- "Keep the ViewModel free of Android Dependencies...This allows me to utilize JUnit unit tests for a quick feedback loop" [[3]](#references)[[7]](#references)
- "ViewModels hold **transient data used in the UI**, but they don’t persist data" [[6]](#references)
- ViewModel class offered by Android survives configuration change (screen rotation) (using Retaining Fragment under the hood). So it can hold UI state [[4]](#references)[[5]](#references)[[7]](#references)

![MVVM](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvvm_viewmodel_scope.png)
[[4]](#references)

- For one-off events (like Toast message), PublishSubject (RxJava) or SingleLiveEvent (Lifecycle Components) [[7]](#references) classes can be used. 
- It can be used by multiple Views
- ViewModel can expose _ObservableInterface<DataState<Data>>_ to hold information about loading, success, error instead of just data. [[7]](#references)


### DataBinding

Pros:
- Reduces boilerplate, because it binds view and logic directly without middle man

Cons:
- In Android, requires full package name to ViewModel class in XML
- In Android, containing logic in XML is not good, it makes testing difficult. Instead, these logics can be moved to custom _BindingAdapters_ [[3]](#references)
- If you want to have click listener for Android View, function in ViewModel has to return _View.OnClickListener_, which forces ViewModel to have Android code


### References

[1] Manoj Jaggavarapu, "Presentation Patterns : MVC, MVP, PM, MVVM," 02 05 2012. [Online]. Available: https://manojjaggavarapu.wordpress.com/2012/05/02/presentation-patterns-mvc-mvp-pm-mvvm/. [Accessed 03 03 2018].

[2] Joe Birch, "Approaching Android with MVVM" 21 09 2015. [Online]. Available: https://labs.ribot.co.uk/approaching-android-with-mvvm-8ceec02d5442. [Accessed 21 10 2020].

[3] Donn Felker, "Android MVVM with DataBinding – Removing Logic from Your Views with BindingAdapters". [Online]. Available: https://www.donnfelker.com/android-mvvm-with-databinding-removing-logic-from-your-views-with-bindingadapters/. [Accessed 21 10 2020].

[4] Luis G. Valle, "Firebase, ViewModels & LiveData" 22 10 2017. [Online]. Available: https://medium.com/@lgvalle/firebase-viewmodels-livedata-cb64c5ee4f95. [Accessed 21 10 2020].

[5] Kamil Seweryn, "MVP to MVVM transformation" 20 01 2018. [Online]. Available: https://proandroiddev.com/mvp-to-mvvm-transformation-611959d5e0ca. [Accessed 21 10 2020].

[6] Lyla Fujiwara, "ViewModels: Persistence, onSaveInstanceState(), Restoring UI State and Loaders" 17 07 2017. [Online]. Available: https://medium.com/androiddevelopers/viewmodels-persistence-onsaveinstancestate-restoring-ui-state-and-loaders-fc7cc4a6c090. [Accessed 21 10 2020].

[7] Jose Alcérreca, "ViewModels and LiveData: Patterns + AntiPatterns" 12 09 2017. [Online]. Available: https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54. [Accessed 21 10 2020].

[8] John Gossman, "Introduction to Model/View/ViewModel pattern for building WPF apps" 08 10 2015. [Online]. Available: https://docs.microsoft.com/en-us/archive/blogs/johngossman/introduction-to-modelviewviewmodel-pattern-for-building-wpf-apps. [Accessed 21 10 2020].

[9] alexy.shelest, "Model View Controller, Model View Presenter, and Model View ViewModel Design Patterns" 03 10 2009. [Online]. Available: https://www.codeproject.com/Articles/42830/Model-View-Controller-Model-View-Presenter-and-Mod. [Accessed 21 10 2020].