# Day 33: Implement a State Machine
#c-fundamentals 
There are a variety of ways to implement a state machine. I give an example below of how to implement a simple state machine to drive a motor.

I begin by defining an enum for the three states in the system: `IDLE`, `MTR_FWD`, and `MTR_BWD`:
```
typedef enum state{
	IDLE,
	MTR_FWD,
	MTR_BWD
} state_t;
```

Next, I define an enum for the three actions, or commands: `CMD_STOP`, `CMD_FWD`, and `CMD_BWD`:
```
typedef enum action{
	CMD_STOP,
	CMD_FWD,
	CMD_BWD
} action_t;
```

Finally, I create the function `motorFsm` which returns the current state of the motor and takes in the arguments `state_t currState` and `action_t action`. Within the function is a switch-case statement that supports three cases for each state (`IDLE`, `MTR_FWD`, and `MTR_BWD`) and a default case for when `currState` is invalid. Within each case statement, I compare the current action with either `CMD_STOP`, `CMD_FWD`, or `CMD_BWD`, print the command, then return the associated states (`IDLE`, `MTR_FWD`, `MTR_BWD`).

```
state_t motorFsm(state_t currState, action_t action){
	switch(currState){
		case IDLE:
			printf("The car is idle!\n");
			if(action == CMD_STOP){
				printf("CMD_STOP has been sent!\n");
				return IDLE;
			}
			else if(action == CMD_FWD){
				printf("CMD_FWD has been sent!\n");
				return MTR_FWD;
			}
			else if(action == CMD_BWD){
				printf("CMD_BWD has been sent!\n");
				return MTR_BWD;
			}
			break;
		case MTR_FWD:
			printf("The car is driving forward!\n");
			if(action == CMD_STOP){
				printf("CMD_STOP has been sent!\n");
				return IDLE;
			}
			else if(action == CMD_FWD){
				printf("CMD_FWD has been sent!\n");
				return MTR_FWD;
			}
			else if(action == CMD_BWD){
				printf("CMD_BWD has been sent!\n");
				return MTR_BWD;
			}
			break;
		case MTR_BWD:
			printf("The car is driving backward!\n");
			if(action == CMD_STOP){
				printf("CMD_STOP has been sent!\n");
				return IDLE;
			}
			else if(action == CMD_FWD){
				printf("CMD_FWD has been sent!\n");
				return MTR_FWD;
			}
			else if(action == CMD_BWD){
				printf("CMD_BWD has been sent!\n");
				return MTR_BWD;
			}
		default:
			printf("Invalid state.");
			break;
	}
	return currState;
}
```

I drive the motor with the code below. I initialize the state to `IDLE`, then create an array of actions, or commands, that simulate a series of commands being sent. I then iterate through the array and call the function `motorFsm`. 

```
int main(){

	// Initialize STATE to IDLE
	state_t STATE = IDLE;
	
	// Create an array to simulate CMDs being sent
	action_t SIM_CMDS[NUM_SIM_CMD] = {CMD_FWD, CMD_STOP, CMD_BWD, CMD_STOP, 
	CMD_BWD, CMD_FWD};
	
	printf("Starting State Machine...\n");
	for(int i = 0; i < NUM_SIM_CMD; i++){
		STATE = motorFsm(STATE, SIM_CMDS[i]);
	}
	
	return 0;
}
```

There are other methods of implementing a state machine, such as 1) a state-transition table 2) an event-driven FSM using function call-backs, which I will go more in detail about in the future.