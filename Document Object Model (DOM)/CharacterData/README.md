# CharacterData
 The **CharacterData** abstract interface represents a Node object that contains characters. This is an abstract interface, meaning there aren't any object of type **CharacterData**: it is implemented by other interfaces, like Text, Comment, or ProcessingInstruction which aren't abstract.

## Properties
Inherits properties from its parent, Node, and implements the ChildNode and NonDocumentTypeChildNode interface.

#### CharacterData.data
Is a DOMString representing the textual data contained in this object.
#### CharacterData.length Read only
Returns an unsigned long representing the size of the string contained in CharacterData.data.
NonDocumentTypeChildNode.nextElementSibling Read only
Returns the Element immediately following the specified one in its parent's children list, or null if the specified element is the last one in the list.
NonDocumentTypeChildNode.previousElementSibling Read only
Returns the Element immediately prior to the specified one in its parent's children list, or null if the specified element is the first one in the list.
## Methods
Inherits methods from its parent, Node, and implements the ChildNode and NonDocumentTypeChildNode interface.

#### CharacterData.appendData()
Appends the given DOMString to the CharacterData.data string; when this method returns, data contains the concatenated DOMString.
#### CharacterData.deleteData()
Removes the specified amount of characters, starting at the specified offset, from the CharacterData.data string; when this method returns, data contains the shortened DOMString.
#### CharacterData.insertData()
Inserts the specified characters, at the specified offset, in the CharacterData.data string; when this method returns, data contains the modified DOMString.
ChildNode.remove() 
Removes the object from its parent children list.
#### CharacterData.replaceData()
Replaces the specified amount of characters, starting at the specified offset, with the specified DOMString; when this method returns, data contains the modified DOMString.
#### CharacterData.substringData()
Returns a DOMString containing the part of CharacterData.data of the specified length and starting at the specified offset.