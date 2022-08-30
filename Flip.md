[[GSAP]]

# FLIP

## Tags:
#gsap 

---

- Provides the animations or transitions i situations when state change couses layout to blink between changes
- **Flip** methods constists of:
	- Fully intergrated with GSAP
	- **First**
	- **Last**
	- **Invert**
	- **Play**
	- For GSAP to know how to animate between states we need to store first and last states
		- getState()
			- records position, scale, rotation properties
			- to keep track of other CSS properties pass a config with props propertie that lists properties to be tracked
				- `.getState(state, { props: 'backgroundColor,color' })`
	- To apply the transition we create a GSAP tween with .from() that apply the described animation on the recorded statae
		- .from() return a timeline so other animations can be intergrated