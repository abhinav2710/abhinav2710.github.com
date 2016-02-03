---
layout: post
categories: project
title: Content Based Video Matching using Spatio-Temporal Volumes
collaborators: Abhinav Garlapati, Adarsh Tadimari, Prof. Sukendhu Das
excerpt_separator: <!--more-->
tags: [Video Classification, Deep Learning, Convolutional Neural Networks]
---
<article>
<h4> Abstract </h4>
Goal of the project is to build a system, which on given a video shot can query for all similar videos in the given dataset and return all the similar videos. We follow the spatio-temporal features presented by <b>Basharat et al.</b> to consturct descriptors from the videos. Based on these descriptors similar videos are matched.
<!--more-->

<h4> Outline </h4>
The major steps in the algorithm are as follows,
<ul>
        <li>Trajectory Generation
        <p>
        We use SIFT features extracted from each frame and generate trajectories. From the SIFT features correspondences, we get the final trajectories using the following steps.
        </p>
        <ul>
                <li> Initial trajectory generation by merging point correspondences </li>
                <li> Removal of irregular trajectory segments </li>
                <li> Merging broken trajectories </li>
                <li> Removal of small trajectories.</li>
        </ul> </li>

        <li> Region Detection </li>
             <p>
                Now that we have trajectories across frames, we wish to perform motion segmentation, for which we perform RANSAC. By performing iterative RANSAC, each time removing a chunk of points which satisfy the same homography, we retrieve various motion segements. After this, we perform clustering as suggested by Basharat et al. We couldn't replicate the performance using the Isodata clustering as suggested by them. After experimenting with various techniques, we use a hierarchical clustering approach which takes a minimum distance between the clusters as a parameter and produces stable clusters.
            </p>
        <li> Region Tracking </li>
             <p>
                We now need to track the regions across the frame. The problems which one comes across in this step is the merging of various clusters or disintegration. We use the two-pass alorithm presented in the paper to propogate labels.
             </p>
        <li> Feature Extraction </li>
             <p> Features were extracted from each of these tracked regions from various cues like Color, Texture. We represent each volume as a feature vector consisting of average color histogram and histogram of gradients of the image.
             </p>
        <li> Feature Comparison and Video Matching </li>
             <p> This step involves computing distances between the obtained descriptors and retrieving videos which have the least distances between the pooled descriptors from each video.</p>
</ul>
<br>
<br>
The full report can be found <a href='../assets/media/st_volumes.pdf'>here</a>.

<br>
<br>
<h4>Example</h4>


<figure>
        <img src='../assets/media/st_vol1.png' alt='missing' />
        <figcaption>Three consecutive frames of a video</figcaption>
</figure>

<figure>
        <img src='../assets/media/st_vol2.png' alt='missing' />
        <figcaption>SIFT interest points in two frames</figcaption>
</figure>

<figure>
        <img src='../assets/media/st_vol3.png' alt='missing' align='middle' width="70%"/>
        <figcaption>Image showing the displacement of the interest point being tracked</figcaption>
</figure>


<figure>
        <img src='../assets/media/st_vol4.png' alt='missing' width="100%"/>
        <figcaption>Filtering and grouping of interest points:
        <br>
              i) All interest points in the image.
        <br>
              ii) Filtered interest points which satisify geometrical consistency conditions.
        <br>
              iii)Region Detection - Using clustering to detect regions which can be tracked.
        </figcaption>
</figure>
              
<h4>References</h4>
<ul>
        <li>Arslan Basharat, Yun Zhai, and Mubarak Shah. Content based video matching using spatiotemporal volumes. Computer
Vision and Image Understanding, 110(3):360–377, June 2008
        </li>
</ul>
</article>
