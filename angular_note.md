Angular Notebook
HTML attribute vs. DOM property

Attributes are defined by HTML. Properties are defined by the DOM (Document Object Model).
 * A few HTML attributes have 1:1 mapping to properties. id is one example.
 * Some HTML attributes don't have corresponding properties. colspan is one example.
 * Some DOM properties don't have corresponding attributes. textContent is one example.
 * Many HTML attributes appear to map to properties ... but not in the way you might think!

 That last category is confusing until you grasp this general rule:
 Attributes initialize DOM properties and then they are done. Property values can change; attribute values can't.


 # Reference
 Angular Guide: https://angular.io/guide/
