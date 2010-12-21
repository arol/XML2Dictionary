# XML2Dictionary

If you have some ideas, conplaints, doubts or something you can contact me at @arolet on Twitter.

*This library is currently in beta version, it has memory leaks and some bugs waiting to be fixed. We (me and my cat) will update soon.*

XML2Dictionary is an object which must be set as NSXMLParser delegate to parse any XML and put it into a NSDictionary.

* The result is an NSDictionary.
* Every node having some child nodes with different names becomes a NSDictionary with structure "node_name" => content.
* Every node having some chidl with same names becomes a NSArray with structure (content,content,content…).
* All chars founded becomes a NSString.

Here goes an example!:
    //Initialize XML2Dictionary
    XML2NSDictionary* parseDelegate = [[XML2NSDictionary alloc] init];

    //Setting up the conection and the parser
    NSURL *url = [[NSURL alloc] initWithString:@"http://some.url/service"];
    NSXMLParser *parser = [[NSXMLParser alloc] initWithContentsOfURL:url];
    
    //Set l'XML2Dictionary as parser delegate
    parser.delegate = parseDelegate;
    
    //Parsejem
    [parser parse];
    
    
    //You can verify the class type of result or its elements with 
    //NSLog(@"%@",[parseDelegate.result class]);
    
    //Now we can navigate through the result
    NSMutableDictionary *xml = parseDelegate.result;
    NSObject *unrecognizedObject = [[[xml valueForKey:@"node1"] 
    								valueForKey:@"node2"] 
    								objectAtIndex:0];

