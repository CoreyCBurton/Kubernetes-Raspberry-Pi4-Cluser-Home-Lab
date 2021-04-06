# Introduction 
While browsing r/homelabs, I ran across a [post](https://www.reddit.com/r/homelab/comments/mbx1l7/my_poe_pi_cluster/) of a cluster build that showed four Raspberry Pis stacked on a platform using Kubernetes. Being completely new to the setup of homelabs, this 
attracted me right away. After researching how to make a similar build, I found out there is a downside to a cluster build using Raspberry Pis. You have to power each Pi using the default plug that came with the unit which makes the build require a lot of cables. 
The solution to this is using a PoE switch and installing PoE hats on the Raspberry Pi. This makes the build more efficient, and I am satisfied with it. There are many ways to have a cluster build with Raspberry Pis and this set up has worked for me.
With Raspberry Pis and all the different hardware they sell, Some people have a unique approach like Jeff Gaerling, in his [youtube video](https://youtu.be/xNndbfxMCLohe),he explains his build which is
worth watching.

# Hardware used in this build 
- 4 [Raspberry Pi 4 4GB Ram](https://www.bestbuy.com/site/canakit-raspberry-pi-4-4gb-starter-pro-kit-premium-black-case/6365737.p?skuId=6365737)
- **please note** This link is to the pro kit, I bought this just in case I want to do anything else with my Pis. 
- 4 [SanDisk Extreme Plus 64GB](https://www.bestbuy.com/site/sandisk-extreme-plus-64gb-microsdxc-uhs-i-memory-card/6282920.p?skuId=6282920)
- **please note** If you buy the pro kit, It comes with a 32 GB sd card.
- 4 [PoE hats with cooling fan](https://www.amazon.com/gp/product/B08PFK6MZJ/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)
- **please note** The fans are loud on this model, other than that, they work great. 
- 1 [Cat 6 Ethernet Cable Six Pack](https://www.amazon.com/gp/product/B01IQWGKQ6/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)
- 1 [NETGEAR 5-Port Gigabit Ethernet Unmanaged PoE Switch](https://www.amazon.com/gp/product/B01MRO4M73/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
- 1 [Techson 4 Layers Clear Acrylic Rack Case for Raspberry Pi 4B / 3B / 3B+](https://www.amazon.com/gp/product/B07TLSVTQP/ref=ppx_yo_dt_b_asin_title_o02_s01?ie=UTF8&psc=1)
- **please note** I found this case to be very medicore. It still works for what needs to be done. 
