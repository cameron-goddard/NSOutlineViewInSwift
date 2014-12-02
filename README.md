NSOutlineViewInSwift
====================

A project to help me understand what is required to provide data for an NSOutlineView control

First up I'll try to get the File system example from the Outline View Programming Guide.

## NSOutlineViewInSwift Project

Option			| Setting
----------		| -----
Table Type		| NSOutlineView
Content View	| Cell Based
Language 		| Swift
IB Method		| Storyboard
Example	from	| [Outline View Programming Topics](https://developer.apple.com/library/mac/Documentation/Cocoa/Conceptual/OutlineView/OutlineView.html)


Steps followed to create the demo (Using Mac OS X Yosemite 10.10.1 and XCode 6)
- Created a new Swift project (Using storyboards cause I like them)
- Add a source list to the content view that has already been created (it is controlled by the ViewController class that has also already been created by the template).
- Mark the ViewController as conforming to the NSOutlineViewDelegate and NSOutlineViewDataSource protocols
- Back in IB link the NSOutlineView datasource and delegate outlets to the view controller (blue circle with white square inside that is at the top of the view)
- Create a new Cocoa class that is a subclass of NSObject. Name it FileSystemItem.
- Convert the Objective-C code from the example over to Swift. This was moderately tricky as the concepts between the two languages sometimes clash. I have tried to keep the code as close to the original as possible for now (though I will likely try and change it to more Swift like idioms once I understand the code better).
- Back in the View Controller I implemented the minimum set of data source methods, the method signatures are shown below in Swift.

	    func outlineView(outlineView: NSOutlineView, 
	    				 child index: Int, 
	    				 ofItem item: AnyObject?) -> AnyObject { }
	    				 
	    func outlineView(outlineView: NSOutlineView, 
	    	   isItemExpandable item: AnyObject) -> Bool { }
	    	   
	    func outlineView(outlineView: NSOutlineView, 
	     numberOfChildrenOfItem item: AnyObject?) -> Int { }
	     
	    func outlineView(outlineView: NSOutlineView, 
	       objectValueForTableColumn: NSTableColumn?, 
	                          byItem:AnyObject?) -> AnyObject? { }

- With all that code filled in the application should run and should try to fill the NSOutlineView in with data. Unfortunately it won't get the path names right because by default the NSOutline view will be set to view based mode where as the example assumes cell based mode.
- In IB select the NSOutlineView (3 clicks). In the Attributes Inspector you can set the Content mode to Cell Based.

Now the application should run and show you the file system in the outline view.


## NSOutlineViewUsingViewMode Project

Option			| Setting
----------		| -----
Table Type		| NSOutlineView
Content View	| View Based
Language 		| Swift
IB Method		| Storyboard
Example	from	| [Outline View Programming Topics](https://developer.apple.com/library/mac/Documentation/Cocoa/Conceptual/OutlineView/OutlineView.html)

There is a version of the same program which uses a view based outline view instead of a cell based view. It should operate exactly the same despite this difference. What needed to be changed between the two programs is listed below

- In IB set the Content Mode for the Outline View to View Based (this is the default)
- The datasource method objectValueForTableColumn: is no longer used. Instead the delegate method viewForTableColumn: is used to generate the content in each row/column. Inside this method we need to create a view to be displayed using makeViewWithIdentifier (look up NSTableView to find it).
- In IB you need to set the Identifier for your NSTableCellView to the string that you used in makeViewWithIdentifier (something like "DataCell")

The application should then run the same as the Cell based version.


