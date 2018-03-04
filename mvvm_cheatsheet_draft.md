# MVVM (Model-View-ViewModel)

- "View : View in MVVM is similar to view in PM. It contains only the UI elements. The interaction between view and ViewModel happens using Data Binding, Commands and Notifications implemented through INotifyPropertyChanged interface.

- ViewModel: View Model is equivalent to PresentationModel in PM pattern, it encapsulates presentation logic and data for the view.  ViewModel contains the state of the view and uses Commands , DataBinding and Notifications to communicate with the view.

- Model: Model is Business logic layer of the application

When you use MVVM pattern for WPF, Silverlight the view wouldn’t have the typical event handlers that’s so common in UI code, All user actions are bound to commands, which are defined in the ViewModel and invoke the necessary logic to update the model. This improves unit testability of MVVM applications." [[1]](#references)

![MVVM](https://raw.githubusercontent.com/jemshit/android_architecture_notes/master/media_files/mvvm.png)
[[1]](#references)





### References

[1] Manoj Jaggavarapu, "Presentation Patterns : MVC, MVP, PM, MVVM," 02 05 2012. [Online]. Available: https://manojjaggavarapu.wordpress.com/2012/05/02/presentation-patterns-mvc-mvp-pm-mvvm/. [Accessed 03 03 2018].


---
Last Edited: 03.03.2018
