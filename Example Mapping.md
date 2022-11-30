[[Programing]]

## Tags:
#programing-concept 

## Links:

---

## Description
- Technique to steer convo to **common understanding**
- Generate rules with examples to assist with **acceptance criteria**
- Can be used to guide **design** and create **tests**
- Can be viewd as contract between parties on behaviour
- Goal is to remove ambiguity in stories
	- Stories are where the bugs begin
- Belongs to Behaviour Driven Development
	- EM is most effective in expansion phase
		- Can be used in extract phase
		- Not suttable for exploration phase
	- [ ] Research Kent Becks 3X

## Value Proposition
- Shared understanding with stakeholders/team
- Design AC together
- Concrete examokes that can be designed and tested
- Help breakup story into smaller segments of work
- Help define ubiquitos language

## Benefits
- Greater quality
	- Becaouse of better understanding
- Greater confidence
	- Faster deployment
	- Increased time to value
- Reduced defects
	- Bugs start with stories, not code

## Usual way of Working
- Bussines, IT and QA are separate
- Small collaboration
- Unclear communication
- Collaborating only when the bugs appear

## Example Mapping WoW
- When all of the groups collaborate missunderstanding can be resolved at the begining of process, when the stories are created

## Crutial Differentiation
- Concepts outlive Parctices outlive tools
	- BDD is concept -> common understanding
	- EM is practice
	- Miro or post-its is a tool for EM impementation

## When to Use
- EM can be used in scenarios where behaciour can be described as rules with examples to illustrate different behaviour
	- Could be used on client
		- when value X selected in dropdown then text field B appears
	- Could be used on API at a high level
		- when call getProfessional the return name
	- Most often used with business logic
		- when status of customer set to Inactive then set payrollEndDate to today
- EM isn't there to create backlog or prioritizing itmes
	- most effective at determining what the capability/responsibility of an API should be
- **Recomended using at last moment before starting a story**

## How It Works
- Understand the problem - User Storu
	- PO writes the user story
	- Change that is needed
	- PO needs to help the team to understand the problem
	- Written in yelow
- Chanllange the problem with questions
	- Questions are written on red
		- Could become new user stories or features
- Indentify Rules
	- For given answer
	- Extract rules from answers
	- writetn in blue
- High level status
	- A lot of red
		- Low understanding -> don't start the story
	- A lot of blue
		- Highly complex stroy
		- Can be broken into smaller stories
		- Can be started
	- A lot of green
		- Why so many examples under on rule
		- Rule can be broke into more rules
		- Can be started