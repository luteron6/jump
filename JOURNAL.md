# jump
Made by: @luteron6

Total hours so far: 30 minutes.

Estimated Cost: $0

## Day 1 - 3:15 PM (30 minutes)

### Background
So I'm a volleyball player. And as a volleyball player, vertical jump is important. So, wouldn't it be great to track your vertical jump height? The answer is OF COURSE! One of my coaches has this device called the OVR Jump, which is a great tool for tracking this metric. 
<p align="center">
  <img src="https://ovrperformance.com/cdn/shop/files/OVRJump2024.11.14.jpg?v=1731545101&width=1000" width="400"><br>The OVR Jump device
</p>

But there's one thing: This device costs $299. It seems really simple. Two bars of technology, and a screen on the middle of them. The product website literally says, "OVR Jump uses laser technology to instantly sense when an athlete is on or off the ground." Upon further research, it is possible to calculate jump height from airtime. I found [this article](https://www.hawkindynamics.com/blog/calculate-jump-height-from-flight-time). In essence, we can calculate jump height based off of the time-of-flight with the equation:

$$
h=\frac{g \cdot t^2}{8}
$$

where<br> h is the vertical height<br> g is gravity (9.81 m/s), and<br> t is the flight time.

So after watching some youtube videos, I found that the long bar and short bar use some sort of IR technology. It basically counts the time from when the plane is unbroken, to when the plane is broken. My project will be to create an open-source vertical jump tracker.
