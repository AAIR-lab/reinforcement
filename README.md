# reinforcement
Carry out the following steps to set up the environment for this assignment.
<ol>
	<li>Clone this repository to your catkin_ws/src.</li>
	<li>Copy all the folders from Models/ and paste it to your ~/.gazebo/Models </li>
	<li>Copy _4__5.jpg and basket.dae from turtle_basket folder to your catkin_ws/src/turtlebot3/turtlbot3_description/meshes/basket. You will need to create the "basket" folder.</li>
	<li> Copy <strike>turtlebot3_waffle.urdf.xacro</strike> turtlebot3_burger.urdf.xacro to your catkin_ws/src/turtlebot3/turtlbot3_description/urdf/ </li>
	<li> You will need to use <strike>"waffle"</strike> "burger" model for this assignment.</li>
	<li>Run catkin_make from your catkin_ws. </li>
	<li>Run source devel/setup.bash from your catkin_ws</li>
	<li>In catkin_ws/src/reinforcement/scirpts/server.py change root_path to your catkin_ws/src/reinforcement. Please use absolute path.</li>
</ol>
<br>
<br>
To start the execution, you will first need to run <b>"server.py"</b>. This will generate a random environment which can be run in Gazebo using launch file <b>"maze.launch"</b>. You can specify the number of subjects using the  argument "-sub". If you want to run the code in headless mode thent use "-headless 1" and to visualize using gazebo use "-headless 0" with the server.py. By default, it will be in the headless mode. "move_tbot3.py" contains services to enable Turtlebot3 to move around if you choose to run the gazebo.
<br>
<ul>
<li>To run server file, execute <b>rosrun reinforcement server.py [options]</b>
	<li>(if not headless mode)To launch maze in gazebo, execute <b>roslaunch reinforcement maze.launch</b></li>
	<li>(if not headless mode)To run move_tbot3.py, execute <b>rosrun reinforcement move_tbot3.py</b></li>
</ul>

The set of actions contains 10 actions. These 10 actions include 5 careful actions and 5 normal actions. The only difference between careful and normal actions is that careful actions have a higher probability of being successful and have a higher cost. These actions include,
<ul>
  <li>careful|normal MoveF: If successful, moves turtlebot3 forward, otherwise turtlebot3 stays still </li>
  <li>careful|normal TurnCW: If successful, rotates turtlebot3 in clockwise direction by 90 degree, otherwise, turtlebot3 rotaes in the opposite direction by 90 degrees. </li>
  <li>careful|normal TurnCCW: If successful, rotates turtlebot3 in counter-clockwise direction by 90 degree, otherwise, turtlebot3 rotaes in the opposite direction by 90 degrees. </li>
  <li>careful|normal pick book_i: If successful, picks the book_i, otherwise no effect. </li>
  <li>careful|normal place book_i bin_k : If successful, places book_i in bin_k </li>
</ul>

Once you put a book in a bin, there is no way to take that book out. When all the books are placed in to some bins, the terminal state is reached. Taking actions in terminal states have no effect on the state and no reward is obtained.

The provided problem API (problem.py) contains following actions.
<ul>
  <li>get_all_actions: returns a list of all possible grounded actions. </li>
  <li>execute_{action_name} {params}: executes the action if feasible. return success_code (1 or -1), next state and reward for the action. </li>
	<li>is_terminal_state {<strike>state</strike>}: returns if the given state is a terminal state or not. </li>
	<li>reset_world : resets the world. (if using gazebo, you need to launch gazebo again). </li>
    </ul>    

<h2>Updates in the code:</h2>
<ul>
	<li>is_terminal_state does not take any arguments now.</li>
	<li>reset_world service added.</li>
	<li>Option added to perform learning without gazebo simulation.</li>
</ul>
