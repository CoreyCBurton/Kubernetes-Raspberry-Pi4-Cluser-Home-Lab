# Introduction 
While browsing r/homelabs, I ran across a [post](https://www.reddit.com/r/homelab/comments/mbx1l7/my_poe_pi_cluster/) of a cluster build that showed four Raspberry Pis stacked on a platform using Kubernetes. Being completely new to the setup of homelabs, this 
attracted me right away. After researching how to make a similar build, I found out there is a downside to a cluster build using Raspberry Pis. You have to power each Pi using the default plug that came with the unit which makes the build require a lot of cables. 
The solution to this is using a PoE switch and installing PoE hats on the Raspberry Pi. This makes the build more efficient, and I am satisfied with it. There are many ways to have a cluster build with Raspberry Pis and this set up has worked for me.
With Raspberry Pis and all the different hardware they sell, Some people have a unique approach like Jeff Gaerling, in his [youtube video](https://youtu.be/xNndbfxMCLohe),he explains his build which is
worth watching.

