# PhylSlider.js
Interactive SVG slider for phylogenetic trees
!(PylSlider.js in action)[sample.jpg]

## What is this ?
In early 2016 I had not found any tree-like SVG slider in javascript. None for the kind of interaction I needed in the demo below. So here it is. 

## Warning : big todo list > contributions welcome !
This is a really cool interaction tool but there is a lot of work to do though : first the javascript is quite ugly since this writing this library was not my primary mean in this project. Moreover :
- the colors of the tags are not yet tweened with the thumb. 
- it has a huge need of a serious viewport handler. 
- there is no real graph design since the tree must be passed all at once, no nice d3-like `node1.add( node2 )` yet.
- as can be first thought, the maximum number of children from the root is limited. On mobile vertical orientation, you cannot have more than 4 children from the root. I have a little idea on how to bypass that problem but it is a very big work and not my priority for now.
- it is hard to imagine nodes with 3 children, though it is not usual in pylogenetics it can be needed. Better keep 2 children as in phylogenetics theory and though you could need it for another use case. It essentially is about design.

For all these reasons contribution are welcome :)

## Demo
astrak.github.io/evolution

## Use
	var tree = {
		content:'H. habilis',
		content0:'Australopithecus',
		content0X:-23,
		content0Y:132,
		mode:'off',
		xStart:10,
		yStart:110,
		xEnd:70,
		yEnd:85,
		tween:{
			tI:[1,0,0,0,0,0,0,0,0,0]
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


