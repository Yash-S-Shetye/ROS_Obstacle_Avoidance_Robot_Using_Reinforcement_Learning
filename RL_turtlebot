#! /usr/bin/env python

import rospy
from std_msgs.msg import Float64
from sensor_msgs.msg import LaserScan
from geometry_msgs.msg import Twist

# Creating a class for all functions

class Turtlebot3RL:
    def __init__(self):
        # initialize ROS node
        self.distToObstacle=0.5
        rospy.init_node('turtlebot3_rl')
        
        # set up ROS publishers and subscribers
        self.cmd_vel_pub = rospy.Publisher('/cmd_vel', Twist, queue_size=1)
        self.laser_sub = rospy.Subscriber('/scan', LaserScan, self.run)
        
        # initialize variables
        self.laser_data = None
        self.reward = None
        self.action = None
        
        # run main loop
        self.run()
    
    # Defining the main function
    def run(self, data):
        rate = rospy.Rate(10) # 10 Hz
        while not rospy.is_shutdown():

            # Sending velocity values to robot wheels
            self.action = Twist()
            self.action.linear.x = 0.2
            self.action.angular.z = 0.5
            
            # send action to robot
            self.cmd_vel_pub.publish(self.action)
            
            # Implementing reward conditions for robot
            # Reward for getting closer to an obstacle and penalize for getting too close
            if data.ranges[300] < self.distToObstacle:
                self.reward = -1.0
            else:
                self.reward = 0.1
            
            rate.sleep()

if __name__ == '__main__':
    try:
        # Calling the main function from class
        Turtlebot3RL()
    except rospy.ROSInterruptException:
        pass
