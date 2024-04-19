## Ticket 101 Code Review
NOTE: Code review is about the code in the `ticket101-code-review` branch, as the `main` branch is updated.
When looking at code line numbers, please make sure you are on the right branch.

### 1 | Requirements & Implementation

The code does not completely work as required, bugs can be found. 

#### UI

It can quickly be noticed that the loan period slider label indicates the range starting from 6,
when the requirements state that allowed loan duration should be >= 12. Slider itself selects the right values, 
label is inaccurate. In addition, the results (approved loan & duration) are not well distinguished from
the input sliders, possibly causing confusion. The results should be enunciated more than the input sliders.
Overall however, the UI is clean and not cluttered.

#### Loan amount correction

This could be considered the biggest shortcoming of the implementation.
The approved loan amount and duration function is not working as expected - when a larger loan is available for the user selected period,
the program does not show the possible larger approved loan. Example case below:


| Personal Code 	| Credit Modifier 	 | Input loan amount   	 | Input loan duration 	 | Expected loan amount 	 | Expected loan duration 	 | Actual loan amount 	 | Actual loan duration 	 | Fault 	                                                                   |
|---------------	|-------------------|-----------------------|-----------------------|------------------------|--------------------------|----------------------|------------------------|---------------------------------------------------------------------------|
|    50307172740 	| 100 	             | 2000    	             | 48	                   | 4800	                  | 	48                      | 	    2000            | 	 48                   | Loan amount is not corrected if selected period allows for a larger loan. |


#### Constraints

It is not explicitly stated in the requirements that the loan duration can be only multiples of 6, nor is it said that loan amount should be fixed to multiples of 100,
yet the implementation has these constraints. 


### 2 | Code

#### Front End

The code itself is clean, organization could use a services and themes folder for a cleaner look, following 
an organization pattern similar to the back-end.

`lib/widgets/loan_form.dart` contains faulty code in lines `41-47`. This faulty updating is the cause of displaying 
wrong loan amounts & durations due to unnecessary conditional. Needs addressing.

#### Back end

The code is well-commented, methods are short, no deep nesting, variable names consistent. Code aesthetics 
are on point. The code is mostly readable, yet some things can be pointed out and corrected.

`ee/taltech/inbankbackend/service/DecisionEngine.java` method `verifyInputs` lines `117-124` use negation for comparisons for no reason,
reducing code readability. Negation should be removed, it is unnecessary.

#### Tests

Both back and front end contain appropriate tests, well done.

