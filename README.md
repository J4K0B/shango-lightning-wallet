# Shango - Lightning Wallet for iOS and Android

## Quick Start

#### 1. Install App
Install the Shango app from Google Play or iTunes App Store. If you received a Beta invitation to test out the cutting edge releases you use these instructions instead 

* iOS Test Flight : https://developer.apple.com/testflight/testers/ for iOS
* Google Play Beta : https://support.google.com/googleplay/answer/7003180?hl=en 

#### 2. Check your node is ready
The first time you connect to the Shango service, you will be assigned a pre-warmed, **full** LND Lightning node that is already pre-synced to the Bitcoin **testnet** blockchain and ready to use. If you get a warning that your chain is not synced it is probably because the cloud service is experiencing high traffic at the moment so just wait until the chain is synced and you see the synched up icon on your dashboard as below. 

![Shango Screenshot](/images/synced.png)

#### 3. Get some Testnet coins
Get some Testnet coins! My usual places to get shiny new testnet coins are listed below. Once your testnet coins have been deposited to your on-chain wallet and confirmed you are ready to spend them. It may take a while to confirm depending on the conditions of the testnet network.

* https://testnet.manu.backend.hamburg/faucet
* https://faucet.lightning.community/

#### 4. Open Channels (optional)
Wait for Channels to open and have the **'Active'** badge near the right. By default autopilot mode is enabled with a commitment of 30% of your funds to open channels. This means that LND will seek out the best nodes to open channels with without any intervention on your part. Relax, your funds may look like they have been spent from your wallet balance but they are actually still in your control and can be redeemed anytime when you close the channels.

However, you may wish to expand beyond what autopilot does by fine tuning whom you open channels with. For example, if you are testing regualrly with a specific crypto exchange, merchant or friend it may be advisable to manually open a channel with them. Try to select counterparties which already have a lot of channels open with others, and remember to set amounts in both directions e.g. have half the balance on your local side and the other half on the remote side. This allows value to move both ways along the channel.

Your goal is to get as 'well connected' as you can, as soon as possible so that you have the highest possible chance of routing payments to/from your node.

#### 5. Spend away!
Try sending an instant Lightning payment to one of the following demo stores:

* https://starblocks.acinq.co/#/
* https://yalls.org/

Note: Whilst opening a channel directly the above sites is optional, it may help you get transfers done faster and save a few Satoshis in fees. 

For Starblocks, the best node to manually open a channel to is this endurance node: 
```03933884aaf1d6b108397e5efe5c86bcf2d8ca8d2f700eda99db9214fc2712b134@34.250.234.192:9735```


## FAQ

#### 1. I'm scared of using cloud services for financial transactions. If Shango is running all the nodes, doesn't that mean you can see all my private keys / access macaroons and get all my funds when you want? What if you get hacked? I FEAR change!!!! 

Chill. Before you run around screaming 'Custodial Wallet! Bad! Bad! Bad!',let us first discuss the long-standing myth and false notion that using cloud services is 'insecure'.

Shango is backed by cloud infrastructure from Amazon Web Services (AWS) - the biggest and most reliable cloud partner on the planet trusted by Fortune 500 companies. According to these links here https://aws.amazon.com/compliance/iso-27001-faqs/ and https://aws.amazon.com/about-aws/whats-new/2018/03/aws-fargate-supports-container-workloads-regulated-by-iso-pci-soc-and-hipaa/ it looks like they have invested a lot into security.

As you can see, they are a ISO 9001, 27001, PCI DSS2, SOC 1, SOC 2, and SOC 3 HIPAA certified data centre for your node authorised to handle the most sensitive data including healthcare and financial information. These are industrial strength facilities with fire suppression, tight physical security and monitored 24x7 by a dedidcated team.

This is in contrast to the false sense of security you get with your privately managed server at home or phone based wallet where anybody can pull the plug accidentally, and has WIFI access to make it easily accessible by hackers outside your door and where any other software installed could be compromising your machine already without you knowing. Granted if you are a security expert you can do a lot to prevent casual hacks but not all of us can or want to do this.

I don't know about you but I personally don't have the time or resources to build industrial strength security into my own private Raspberry Pi node and if my money was truly at stake  I would much rather be trusting a professional service than myself any day. Not that AWS is unhackable, but the chances are far less and and at the end of the day, if they get hacked you will be in the same boat as giants like Verizon, Netflix, Comcast etc and you have a much better case suing them for damages than trying to get back your funds you lost from your Windows PC.

Now since you know my stance on cloud computing, we can talk about the 
security measures we have put in place. Shango is built around portable, stateless docker containers managed by the ECS FARGATE service from AWS. This means that :

- Nobody, not even me has access to the underlying infrastructure of the nodes. i.e. There is no individual server you can attack as it is spread scross multiple zones and computing resources and changes at any time.

- Once the node shuts down, all the data is lost forever so there is no trace of your private information

- All the LND folders are (at the time of writing, this is still in development and pending the release of the new LND version 0.42) encrypted with a passphrase set by YOU. That means that even if someone did get access to the files, they would be unable to read them without your passphrase. 

- All the data is backed up on your device. Since there is no persistent storage on Fargate containers, Shango makes it easy to export your entire node as a portable docker (https://www.docker.com/what-docker) container that you can take to your own Home PC, another host like Digital Ocean etc whenever you want. So even if the Shango services shuts down you still have your node in tact. The original docker images for LND were around 1GB but with a bit of tweaking we got it down to 13MB compressed which is the size of most high def photos you may already have on your phone. You can easily back this up and keep it somewhere safe and launch a Linux based LND node from anywhere you like.






