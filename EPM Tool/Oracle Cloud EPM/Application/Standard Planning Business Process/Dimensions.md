Are the key structural components in EPM Planning
# Required Dimensions 
Rrequired Dimensions includes: 
	Account
	Entity
	Scenario
	Version
	Period
	Year
	Currency (if the application is multicurrency)
# Custom Dimensions
Custom Dimensions (can be created up to 32 custom dimensions) such as:
	Product
	Customer
	Geography
	Channel
	Employee
	
User-Defined custom dimensions cannot be deleted
# Dimensions properties 
define how each member within each dimension behaves and displays

**Two Pass Calculation** checkbox: recalculates value of members based on values of parent members or other members, available for account and entity members with dynamic calc and store properties #TwoPassCalculation 
Apply Security checkbox: Allow security to be set on the dimension members (if leave uncheck, this dimensions will be access by users without restriction.
	Mus be selected before assigning access rights to dimension members
Data Storage option: Default to **Never Share**
Display Option: Default to **Member Name**
Hierarchy Type is available for dimensions bound to an aggregate storage cube.
Cube: Select which cube the dimension is valid

# Dimension: Hierarchy
Structure Data for Analysis - Organize related data elements into logical parent-child relationship
Enable drill-down reporting - Navigate from summary to detailed data, support insight generation
Supports Aggregations - Summarize and calculate data at various hierarchy levels

Three ways to reference members : 
Genealogy: describe how members relate like a family tree 
![[Pasted image 20261008145101.png]]

Generations and lelves: help locate a member's position relative to the top of the hierarchy
	Generations: start at number 1 at the dimension name and increase as move down the hierarchy
	Levels: also reffered as leaf nodes or base members. Start with 0 and increase as moving up the hierarchy. Level number are **relative** to their respective hierarchy
![[Pasted image 20261008145634.png]]

Hierarchy Aggregations and Calculations based on aggregation options: 
![[Pasted image 20261008145841.png]]