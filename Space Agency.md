# Space Agency

## Tags:
#frontend, #react, #animation, #learning, #typescript, #gsap, #sideproject 

## Description
- Main goal was to create responsive web app for space agency
	- Designs were provided throught [[Figma]]
- Reason for the sideproject was to deepen the knowlage of [[React]] and [[Typescript]] as well as to learn to use [[GSAP]]

### Acronims
Animation Area - AA
Animation Element - AE
Parent Element - PE
Selected Element - SE
Current Element - CE

## TODO:
- [x] **Animation Area**
	- [x] Area which limits the space where the animate element can move
		- [x] Movment is being restricted b/c movment is being animated
	- [x] All changes to AA properties are not animated, the are instant mutations
	- [z] AA beeds to be able to change in horizontal and vertical direction
	- [x] AA needs to be separate component that has child prop which is AE
	- [x] AA needs to be able to handle AE of diferent dimensions
		- [x] So that it works with exploratory funcionality
	- [x] Animation interuption results in skipping to the end  of the animation
		- [x]  Animation interuption is when the NavButton is clicked whilre animation is still running
- [x] **Explore Walkthrough**
	- [X] When Eplore button is clicked app does the tour of the pages
	- [x] Exploration can be stoped
		- [x] Place the exploration controller besides the logo
			- Preferably a play/pouse/stop button
		- [x] Pausing prevents setTimeout for exploration to take effect
			- Custom hook doesn't work for pausing exploration
				- b/c of strange behaviour around states and their updating or maybe b/c of the values the flags had at the moment the setTimeout was called
				- [[setTimeout Callback]]
			- [x] Try migrating the functionality to ExplorationProvider
				- start, pause and stop/reset will be controled by dispathces
					- [x] exploration can be started
						- exploration starts scroling through the pages
					- [x] exploration can be paused
						- exploration is stoped without scrolling to next page
					- [x] exploration can be unpaused
						- exploration continues scrolling from the current point
					- [x] exploration can be stoped
						- exploration can't be unpaused
						- exploration can only be started again from the home page
	- [x] ExplorationController has animation
- [ ] **Routing Transition**
	- [ ] Background will slide
	- [[Flip]]
	- [Example](https://codesandbox.io/s/6l1li?file=/src/index.tsx)
		- [x] Disable slider animation to focus on Page transition
		- [x] CSSTranistion used for page transition calls onEntering and onExit
		- [x] Get the page HTML node that can be used in onEntering and onExit to animate the page
		- [x] Be able to determine the next page
		- [x] In the direction that depends on that page position in the NavBar
			- [x] General fade transition
			- [x] Sliding animation
			- [x] Navigational elements should stay fixed, all else has animation applyed
				- [x] Navigational elements of different pages move when switching between pages
					- [x] You can specify the classes that are excluded from the animation
				- [x] Make animation change direction deppending on intra page animation direction
					- [x] Make animation directional agnostic
						- [x] Replace horizontal/vertical intra page animation methods with one generalized method
				- [x] Generalize page animation to be covered by single method
				- [x] Change AnimationRouteTransitionType to have `duration` instead of `timeout`
					- [x] Make the animations use the duration in the tweens
		- [x] Background only slides when on inter page animation
			- On intra page animation backgroud stays and elements move
		- [ ] Make planets glow or to be spining slightly
			- [Moon](https://www.youtube.com/watch?v=sNUNB6CMnE8)
			- [Mars](https://www.youtube.com/watch?v=qiqIP-altNM)
			- [Europa](https://sos.noaa.gov/catalog/datasets/europa-jupiters-moon/)
		- [ ] Make page transitions be like fast mooving sliding with stars passing by
		- [ ] Add aditional images in slide transition
			- [ ] Asteroids
			- [ ] Planets
			- [ ] Satelites
	- [ ] Apply appropriate changes to the small screens
- [ ] Add mouse based paralax animation
- [ ] Add horizontal scroll to the whole page
		