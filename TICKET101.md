## Ticket 101 Code Review

### 1 Requirements & Implementation

The code does not completely work as required, bugs can be found. 

#### UI

It can quickly be noticed that the loan period slider label indicates the range starting from 6,
when the requirements state that allowed loan duration should be >= 12. Slider itself selects the right values, 
label is inaccurate. In addition, the results (approved loan & duration) are not well distinguished from
the input sliders, possibly causing confusion. The results should be enunciated more than the input sliders.
Overall, the UI is clean and not cluttered.

#### Loan amount correction

The approved loan amount and duration function is not working as expected - when a larger loan is available for the user selected period,
the program does not return the possible larger approved loan. Example case below:


| Personal Code 	| Credit Modifier 	 | Input loan amount   	 | Input loan duration 	 | Expected loan amount 	 | Expected loan duration 	 | Actual loan amount 	 | Actual loan duration 	 | Fault 	                                                                   |
|---------------	|-------------------|-----------------------|-----------------------|------------------------|--------------------------|----------------------|------------------------|---------------------------------------------------------------------------|
|    50307172740 	| 100 	             | 2000    	             | 48	                   | 4800	                  | 	48                      | 	    2000            | 	 48                   | Loan amount is not corrected if selected period allows for a larger loan. |


#### Constraints

It is not stated in the requirements that the loan duration can be only multiples of 6, nor is it said that loan amount should be fixed to multiples of 100.


### 2 Code

#### Front End

The code itself is clean, organization could use a services and themes folder for a cleaner look, following 
an organization pattern similar to the back-end.

#### Back end

The code is well-commented, methods are short, no deep nesting, variable names consistent. Code aesthetics 
are on point. The code is mostly readable, yet some things should be pointed out and corrected.

`ee/taltech/inbankbackend/service/DecisionEngine.java` method `calculateApprovedLoan` lines `54-62` contains logic for 
determining the loan amount or duration. The logic is confusing, faulty and the code could be extracted as a new method for readability.

`ee/taltech/inbankbackend/service/DecisionEngine.java` method `verifyInputs` lines `117-124` use negation for comparisons for no reason,
reducing code readability. Negation should be removed, it is unnecessary.
