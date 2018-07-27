# Subject


Given a subject , you can subscribe to it , providing an Observe , which will start receiving values normally . From the perspective of the Observe, it cannot tell whether the Observable execution is coming from a plain unucast Observable or a Subject.

Internally to Subject , subscribe does not invoke a new execution that delivers values . It simply registers the given Observer in a list of Observers, similarly to how addListener usually works in other libraries and languages.

