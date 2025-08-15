# jump
Made by: @luteron6

Total hours so far: 3 hours

Estimated Cost: $66.55 (plus tax and shipping)

## Day 1 - 8/14/2025 - 3:15 PM (1 hour)
### Background
So I'm a volleyball player. And as a volleyball player, vertical jump is important. So, wouldn't it be great to track your vertical jump height? OF COURSE! One of my coaches has this device called the OVR Jump, which is a great tool for tracking this metric.
<p align="center">
  <img src="https://ovrperformance.com/cdn/shop/files/OVRJump2024.11.14.jpg?v=1731545101&width=1000" width="400"><br>The OVR Jump device
</p>

But there's one thing: This device costs $299. It seems really simple. Two bars of technology, and a screen on the middle of the long one. The product website literally says, "OVR Jump uses laser technology to instantly sense when an athlete is on or off the ground." The first thing I thought when I saw it was, "I can make that". So this is my attempt to make one. Upon further research, it is possible to calculate jump height from airtime. I found [this article](https://www.hawkindynamics.com/blog/calculate-jump-height-from-flight-time). In essence, we can calculate jump height based off of the time-of-flight with the equation:

$$
h=\frac{g \cdot t^2}{8}
$$

where<br> *h* is the vertical height<br> *g* is gravity (9.81 m/s), and<br> *t* is the flight time.

So after watching some Youtube videos, looking at the [product description](https://ovrperformance.com/products/ovr-jump), and reading the [manual](https://cdn.shopify.com/s/files/1/0791/9622/5826/files/OVR_Jump_User_Manual.pdf?v=1734878083), I found that the long bar and short bar use some sort of IR technology. It basically creates a light curtain between the bars, and can see your feet in that plane. When you jump, your feet disappear, and the plane goes from broken to unbroken. The devices measures the time between your takeoff and landing to calculate the user's vertical. My project will be to create an open-source vertical jump tracker.

The explanation above of the OVR Jump might be confusing, so let me explain that graphically:

<p align="center">
  <img src="https://github.com/user-attachments/assets/1f2ef984-af54-4bae-a6f9-a458d3fd4cfc" width="800"><br>The concept
</p>

If we can measure the time-of-flight (TOF), we can calculate the vertical jump. We know the TOF occurs when the device can no longer see the user's feet and the plane is unbroken. In other words, we measure the time between broken planes. For example, if my feet disappear (from the perspective of the device) for 0.7 seconds, my TOF is 0.7 seconds. Plugging that into the equation above gives a vertical of 0.6008 meters. Converting that to inches (because I'm American), gives a vertical of 23.6 inches. So the goal of this project is to build a device that can measure this time-of-flight.

## Day 2 - 8/15/2025 - 9:54 (2 hours)
So today I've been looking for parts to make the actual laser curtain device. I found these [IR Break Beam Sensors](https://www.adafruit.com/product/2168) from Adafruit:

<p align="center">
  <img src="https://cdn-shop.adafruit.com/970x728/2168-04.jpg" width="400"><br>IR Break Beam Sensors
</p>

The thing is, these are expensive. They go for $5.95, and if I have 4, that'll be $23.80. We'll see. The transmitters will go in their own box, and the receivers will go with a microcontroller.

But first, let's discuss the transmitter box. In the transmitter box, we'll put a [battery](https://www.adafruit.com/product/258) and a [latching switch](https://www.amazon.com/Gebildet-Prewired-Waterproof-Self-Locking-Stainless/dp/B0BXPFW69R/) to turn the LEDs on and off. We also need some way to charge the battery, so I'll add a [USB-C charger](https://www.adafruit.com/product/4410).

<table align="center" border="0" cellspacing="0" cellpadding="10">
  <tr>
    <td align="center">
      <img src="https://cdn-shop.adafruit.com/970x728/258-02.jpg" height="300"><br>
      battery
    </td>
    <td align="center">
      <img src="https://m.media-amazon.com/images/I/61wo18ZkgVL._AC_SX425_PIbundle-3,TopRight,0,0_SH20_.jpg" height="300"><br>
      latching switches
    </td>
    <td align="center">
      <img src="https://cdn-shop.adafruit.com/970x728/4410-04.jpg" height="300"><br>
      charging board
    </td>
  </tr>
</table>

So the BOM currently is:
* [IR Sensors](https://www.adafruit.com/product/2168): $23.80 ($5.95x4)
* [Battery](https://www.adafruit.com/product/258): $9.95
* [Latching Switch](https://www.amazon.com/Gebildet-Prewired-Waterproof-Self-Locking-Stainless/dp/B0BXPFW69R/): already owned ($7.99 for 3)
* [Charging Board](https://www.adafruit.com/product/4410): $5.95

The other half shouldn't be too hard. It'll be similar, but including a microcontroller to measure break time, and an OLED to display the calculations.
If I stick to Adafruit, I found the [Adafruit Feather RP2040](https://www.adafruit.com/product/4884):

<p align="center">
  <img src="https://cdn-shop.adafruit.com/970x728/4884-07.jpg" width="400"><br>Adafruit Feather RP2040
</p>

It has can charge a battery via the USB-C port, so I won't have to get another charging board. It'll also need another battery and on/off switch. However, Adafruit suggests the IR be powered with 5v, so I need some sort of step-up. I found [this one](https://www.adafruit.com/product/4654/).
It also needs a 0.96" OLED display, and I have one already.
So the items I need to add to the BOM are:
* [Adafruit Feather RP2040](https://www.adafruit.com/product/4884): $11.95
* [another battery](https://www.adafruit.com/product/258): $9.95
* [Adafruit MiniBoost 5V @ 1A](https://www.adafruit.com/product/4654): $3.95
* 0.96" OLED Display: already owned (~$2.50)
* Total Estimated Cost: $66.55 (plus tax and shipping)
