---
layout: post-left
title: "Instructions for Decoding SOC-i’s Radio Transmissions"
date: 2022-03-15 00:00:00
author: A&ampA CubeSat Team
permalink: /communications.html
category: missions soc-i attitude-control optimal-control convex-optimization optimal-spacecraft-attitude-motion
icon: fa-book-open
---
<!-- BACKGROUND -->
<section class="wrapper style2 container">
    <header> <h2>Background</h2> </header>
    <p>
        The Satellite for Optimal Control and Imaging (SOC-i) will use a Pacific Crest XDL Micro Transceiver. The XDL radio can only transmit using a limited number of transmission protocols, none of which are commonly used and have little to no publicly available documentation. This document describes how anyone can decode SOC-i’s telemetry.
    </p>
</section>
<!-- SECTION 2 -->
<section class="style4 wrapper container">
    <header><h2>How to Receive a Beacon</h2></header>
    <p>
        SOC-i will transmit its telemetry beacon once per minute if it is in a nominal operating mode.
    </p>

    <header><h1>Finding SOC-i</h1></header>
    <p>
        Thanks to NORAD, a two line element (TLE) for SOC-i will be available at <a href="https://www.celestrak.com/NORAD/elements/">celstrak.com</a> after SOC-i launches. With a TLE, one can how to point your antenna to receive SOC-i’s transmission. <a href="https://www.amsat.org/keplerian-elements-resources">The AMSAT website</a> explains how to do this.
    </p>

    <header><h1>Link Margin</h1></header>
    <p>
        To accurately demodulate SOC-i’s beacon, a signal to noise ratio of about 10 dB is required. SOC-i will be in a 555 km orbit, and will transmit with an EIRP between 23.2 dBm and 27.7 dBm (depending on where SOC-i is pointing its antenna). It will transmit between 435 MHz and 438 MHz. This should provide enough information to determine if a ground station will have enough gain to demodulate SOC-i’s beacon. You will need to factor in the gains and losses of your ground station. Also note that SOC-i is only555 km when it is directly overhead, and is actually over 2,000 km away when it is near the horizon, so keep this in mind when you calculate free space path losses. For a comparison, this <a href="https://docs.google.com/spreadsheets/d/1LnmVq8DV7MKtmCDrb-FcXqUdP9y6fdAOcGNFGtgSXoE/edit?usp=sharing">link</a> describes our link margin calculations in greater detail. We plan on using an ICOM 9100 radio with a 13 dBi Yagi antenna, and our calculations show that we have a suitable signal to noise ratio.
    </p>

    <header><h1>Sample Recording</h1></header>
    <p>
        Check out our <a href="https://github.com/AA-CubeSat-Team/decoding">GitHub page</a> where you can use our code to test out receiving a sample recording from SOC-i’s radio! This page includes our code to demodulate and unpackage transmissions from SOC-i and describes this process with the sample recording.
    </p>
</section>

<!-- SECTION 3 -->
<section class="style4 wrapper container">
    <header><h2>Demodulation</h2></header>
    <p>
        There are many ways to demodulate a signal from SOC-i. One way would be to usea radio which is already capable of demodulating FM signals, such as the ICOM-9100. Another way will be to simply record the baseband signal, using a software defined radio, and submit the IQ signal to our website where it will be automatically demodulated and decoded. This feature is currently a work in progress, however. An IQ signal can also be demodulated using GNU Radio companion, which can be downloaded at this <a href="www.gnuradio.org/">link</a> or any other demodulation software.
    </p>

    <br/>
    <p>
        The baseband signal (absolute value of IQ vectors):
    </p>
    <center>
        <div class="5u">
            <a href="#" class="imagenb featured"><img src="/images/Figure1.png" /></a>
        </div>
        <header>Figure 1: A packet received from SOC-i</header>
    </center>

    <br/>
    <p>
        The demodulated packet:
    </p>
    <center>
        <div class="6u">
            <a href="#" class="imagenb featured"><img src="/images/Figure2.png" /></a>
        </div>
        <header>Figure 2: Demodulated Bits</header>
    </center>
    
</section>

<!-- SECTION 4 -->
<section class="style4 wrapper container">
    <header><h2>Decoding</h2></header>
    <p>
        Once you have demodulated the signal into bits, you need to decode the bits to determine the message sent by SOC-i. Each transmission is sent as a single packet. The start of the packet is the preamble, which is a series of 142 alternating pairs of 1’s and 0’s (284 total):
    </p>
    <center>
        <p>Preamble: [1 1 0 0 1 1 0 0 1 1 0 0 1 1 0 0 1 1 ...]</p>
    </center>
    <p>
        The full preamble is shown in figure 3.
    </p>
    <center>
        <div class="6u">
            <a href="#" class="imagenb featured"><img src="/images/Figure3.png" /></a>
        </div>
        <header>Figure 3: The Preamble, bits 1-284</header>
        <br/>
        <br/>
        <div class="6u">
            <a href="#" class="imagenb featured"><img src="/images/Figure4.png" /></a>
        </div>
        <header>Figure 4: The Message, bits 285-725</header>
    </center>

    <br/>
    <p>
        After the preamble, the radio sends 5 header bytes (the team is communicating with Trimble to learn what these 5 bytes are used for), and 49 data bytes, for a total of 54 bytes. The 54 bytes are sent 18 bytes at a time in three blocks, and are interleaved together. The interleaving pattern for one block of 18 bytes is described below:
    </p>
    <center>
        <p>Bytes Sent = [A B C D E F G H I J K L M N O P Q R]</p>
        <br/>
        <p>Bits Received = [× × A1 B1 C1 ... × × A2 B2 C2 ... × × A3 B3 C3 ... × × P8 Q8 R8]</p>
    </center>
    <br/>
    <p>
        For the first block, bytes A,B,C,D and E are the header bytes. The subscripts on each byte represent the bit number in the byte. The ×represents separating bits (the pairsof separating bits are a 1 and a 0 or a 0 and a 1), and can be ignored. Therefore, 18 interleaved bits form a block of 160 bits. The algorithm in figure 5 shows how the bits can be de-interleaved:
    </p>
    <br/>
    <center>
        <div class="6u">
            <a href="#" class="imagenb featured"><img src="/images/Figure5.png" /></a>
        </div>
        <header>Figure 5: De-interleaving Algorithm</header>
    </center>

    <br/>
    <p>
        Each packet contains three of these blocks. With the de-interleaving algorithm, the message from figure 2 can be decoded! For example, the first block (bits 285-445) in hexadecimal is:
    </p>
    <center>
        <p>[90 00 09 1F 7C 92 FF F8 00 50 49 72 8C AF 6C 80 17 06 06 62]</p>
    </center>
    <p>
        And when de-interleaved becomes:
    </p>
    <center>
        <p>[01 E0 0C 00 24 48 65 6C 6C 6F 20 77 6F 72 6C 64 21 20]</p>
    </center>
    <br/>
    <p>
        The first 5 bytes here are the header bytes, and can be ignored for now. The two remaining blocks after being de-interleaved become:
    </p>
    <center>
        <p>[54 68 69 73 20 69 73 20 53 30 43 2D 49 21 20 47 6F 6F]</p>
        <br/>
        <p>[64 62 79 65 21 66 66 66 66 66 66 66 66 66 66 66 66 66]</p>
    </center>
    <br/>
    <p>
        We ignore the final 13 bytes in block 3, since our message is only 36 bytes long. Thus our message is decoded! If we convert the bytes to ASCII characters, we recover SOC-i’s message:
    </p>
    <center>
        <div class="6u">
            <a href="#" class="imagenb featured"><img src="/images/Figure6.png" /></a>
        </div>
        <header>Figure 6: A Message From SOC-i</header>
    </center>

    <br/>
    <p>
        The packet also contains reed-solomon error correction bytes at the end of the packet. The team is currently working on a code which will use these bytes for error correction.
    </p>

</section>

<!-- SECTION 5 -->
<section class="style4 wrapper container">
    <header><h2>Parsing Telemetry</h2></header>
    <p>
        The bytes in the telemetry beacon will include information about the cubesat’s battery voltages, operating mode, attitude, rotation rate and more. You will be able to parse these bytes using a table from our website. However, this is still a work in progress.
    </p>                
</section>

<!-- SECTION 6 -->
<section class="style4 wrapper container">
    <header><h2>Submitting Telemetry to the AACT Website</h2></header>
    <p>
        You will also be able to submit this telemetry to our website. This feature is still a work in progress.
    </p>                
</section>


