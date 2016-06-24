# PhylSlider.js
An interactive SVG slider for phylogenetic trees.

<img alt="PhylSlider.js in action" src="https://github.com/Astrak/PhylSlider.js/blob/master/sample.jpg?raw=true"/>

## What is this ?
Seems javascript does not have any library for this, so here it is. Better experience than blabla : [see the demo](https://astrak.github.io/evolution).

## Warning : big todo list > contributions welcome !
This is a really cool interaction tool but there is a lot of work to do though : first the javascript is quite ugly since this writing this library was not my primary mean in this project, I stopped working on it as soon as it did the job. Moreover :
- the colors of the tags are not yet tweened with the thumb. 
- it needs a viewport handler : first a little function to set the correct `viewBox` depending on the viewport's width. But it could also change depending on mobile orientation, since this tool takes some place on a mobile screen. But it would also change the page layout so the developper may prefer to set that himself. In the demo that is what I did on horizontal orientation : the new layout is changed outside PhylSlider.js.
- there is no real graph design since the tree must be passed all at once, no nice d3-like `node1.add( node2 )` yet.
- as can be first thought, the maximum number of children from the root is limited. On mobile vertical orientation, you cannot have more than 4 children from the root with biggest screens. I have a little idea on how to bypass that problem but it is a very big work and not my priority for now.
- not sure if branches should arrive to their nodes, or if the script should check if nodes have children to draw branches that come from them.
- it is hard to imagine nodes with 3 children and it is not usual in pylogenetics. Better keep 2 children as in phylogenetics theory and though you could need it for another use case. It essentially is about design for now.

For all these reasons it is a complex feature and contribution are welcome :)

## Use
	var tree = {
		content:'H. habilis',
		content0:'Australopithecus',        //the node branch is the one that arrives to it. Content0 is an optional
		content0X:-23,                      //tag for the beginning of this branch.
		content0Y:132,                      
		mode:'off',                         //tells whether the thumb can slide on that node's branch. Since it is
		xStart:10,                          //the root branch that arrives to the first node, it is disabled.
		yStart:110,
		xEnd:70,
		yEnd:85,
		tween:{
			tI:[1,0,0,0,0,0,0,0,0,0]        //tween can have multiple properties which can be numbers or arrays
		},
		children:[
			...
		]
	};
	var slider = new PhylSlider({
		tree:tree,
		width:340, height:145,
		fontSize:20,
		fontFamily:'Arial',
		bezier:false,
		color:'#333',
		colorOff:'#222',
		strokeWidth:8,
		switchableStyle:false,              //adds a button to switch parent-child lines from straight line to bezier
		callback:function ( tween ) {       //example of callback used in the threejs demo above
			if ( mesh ) mesh.morphTargetInfluences = tween.tI;
			camera.update = renderer.shadowMap.needsUpdate = true;
		}
	});

	slider.setThumb( 'H. habilis' );        //sets the initial active tree node