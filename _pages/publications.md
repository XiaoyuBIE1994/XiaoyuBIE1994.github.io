---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

<!-- {% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %} -->
<style>
* {
  box-sizing: border-box;
}

/* Create two unequal columns that floats next to each other */
.column {
  float: left;
  padding: 0px;
}

.left {
  align-items: top;
  width: 30%;
}

.right {
  align-items: top;
  width: 68%;
}

.middle {
  align-items: top;
  width: 2%;
}
/* Clear floats after the columns */
.row:after {
  content: "";
  align-items: top;
  display: table;
  clear: both;
}

.content figure {
       width: 90%;
       display: flex;
       align-items: top;
       overflow: hidden;
       margin-left: auto!important;
       margin-right: auto!important;
      }
</style>

Here is a selection of recent publications, full list can be found on [Google Scholar](https://scholar.google.com/citations?user=Ymz1-_0AAAAJ&hl=en)  
\* indicates equal contribution.

<!-- 2025 ICASSP SD-Codec-->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../sdcodec/resources/images/teaser.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>Learning Source Disentanglement in Neural Audio Codec</b><br>
        <b>Xiaoyu BIE</b>, Xubo Liu, Gaël Richard<br>
        <i>IEEE International Conference on Acoustic, Speech and Signal Procssing (<b>ICASSP</b>), 2025</i><br>
        <a href="https://arxiv.org/abs/2409.11228" target="_blank">[arXiv]</a>
        <a href="https://xiaoyubie1994.github.io/sdcodec" target="_blank">[Project page]</a>
        <a href="https://github.com/XiaoyuBIE1994/SDCodec" target="_blank">[Code]</a>
      </p>
    </div>
  </div>
</article>

<!-- 2022 arXiv HiT DVAE-->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../images/publications/2022_HiT_DVAE.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>HiT-DVAE: Human Motion Generation via Hierarchical Transformer Dynamical VAE</b><br>
        <b>Xiaoyu BIE*</b>, Wen Guo*, Simon Leglaive, Laurent Girin, Francesc Moreno-Noguer, Xavier Alameda-Pineda<br>
        <i>arXiv preprint arXiv:2204.01565</i><br>
        <a href="https://arxiv.org/abs/2204.01565" target="_blank">[arXiv]</a>
      </p>
    </div>
  </div>
</article>

<!-- 2022 TASLP DVAE SE-->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../images/publications/2022_TASLP_DVAE-SE.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>Unsupervised Speech Enhancement using Dynamical Variational Auto-Encoders</b><br>
        <b>Xiaoyu BIE</b>, Simon Leglaive, Xavier Alameda-Pineda, Laurent Girin<br>
        <i>IEEE/ACM Transactions on Audio, Speech and Language Processing (<b>TASLP</b>), 2022.</i><br>
        <a href="https://arxiv.org/abs/2106.12271" target="_blank">[arXiv]</a>
        <a href="https://ieeexplore.ieee.org/document/9894060" target="_blank">[Paper]</a>
        <a href="https://team.inria.fr/robotlearn/unsupervised-speech-enhancement-using-dynamical-variational-auto-encoders/" target="_blank">[Project page]</a>
        <a href="https://github.com/XiaoyuBIE1994/DVAE_SE" target="_blank">[Code]</a>
        <img src="https://img.shields.io/github/stars/XiaoyuBIE1994/DVAE_SE.svg">
      </p>
    </div>
  </div>
</article>

<!-- 2022 ExPI-->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../images/publications/2022_CVPR_ExPI.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>Multi-Person Extreme Motion Prediction</b><br>
        Wen Guo*, <b>Xiaoyu BIE*</b>, Xavier Alameda-Pineda, Francesc Moreno-Noguer<br>
        <i>IEEE/CVF Conference on Computer Vision and Pattern Recognition (<b>CVPR</b>), 2022.</i><br>
        <a href="https://arxiv.org/abs/2105.08825" target="_blank">[arXiv]</a>
        <a href="https://openaccess.thecvf.com/content/CVPR2022/html/Guo_Multi-Person_Extreme_Motion_Prediction_CVPR_2022_paper.html" target="_blank">[Paper]</a>
        <a href="https://team.inria.fr/robotlearn/multi-person-extreme-motion-prediction" target="_blank">[Project page]</a>
        <a href="https://zenodo.org/record/5578329#.Ya_TCvGZP0q" target="_blank">[Dataset]</a>
        <a href="https://github.com/GUO-W/MultiMotion" target="_blank">[Code]</a>
      </p>
    </div>
  </div>
</article>

<!-- 2021 FnT DVAE -->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../images/publications/2021_FnT_DVAE.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>Dynamical Variational Autoencoders: A Comprehensive Review</b><br>
        Laurent Girin, Simon Leglaive, <b>Xiaoyu BIE</b>, Julien Diard, Thomas Hueber, Xavier Alameda-Pineda<br>
        <i>Foundations and Trends in Machine Learning, 2021, Vol. 15, No. 1-2, pp 1–175.</i><br>
        <!-- <i>Foundations and Trends in Machine Learning, To appear.</i><br> -->
        <a href="https://arxiv.org/abs/2008.12595" target="_blank">[arXiv]</a>
        <a href="https://www.nowpublishers.com/article/Details/MAL-089" target="_blank">[Paper]</a>
        <a href="https://team.inria.fr/robotlearn/dvae/" target="_blank">[Project page]</a>
        <a href="https://www.youtube.com/watch?v=-Ix8k6BVOeU&list=PLuZsCU0LDHDeEusitbdY6bNKOEhqh6DnS&t=5s" target="_blank">[Tutorial]</a>
        <a href="https://github.com/XiaoyuBIE1994/DVAE" target="_blank">[Code]</a> 
        <img src="https://img.shields.io/github/stars/XiaoyuBIE1994/DVAE.svg">
      </p>
    </div>
  </div>
</article>

<!-- 2021 Interspeech DVAE -->
<article class="row">
  <div class="column left">
    <figure class="image">
      <img src="../images/publications/2021_Interspeech_dvae-speech.png" width="100%">
    </figure>
  </div>
  <div class="column middle">
    <figure class="image">
      <img src="../images/blank_placeholder.png" width="100%">
    </figure>
  </div>
  <div class="column right">
    <div class="content">
      <p>
        <b>A Benchmark of Dynamical Variational Autoencoders applied to Speech Spectrogram Modeling</b><br>
        <b>Xiaoyu BIE</b>, Laurent Girin, Simon Leglaive, Thomas Hueber, Xavier Alameda-Pineda<br>
        <i><b>Interspeech</b>, 2021.</i><br>
        <a href="https://arxiv.org/abs/2106.06500" target="_blank">[arXiv]</a>
        <a href="https://www.isca-speech.org/archive/interspeech_2021/bie21_interspeech.html" target="_blank">[Paper]</a>
        <a href="https://team.inria.fr/robotlearn/interspeech21-dvae/" target="_blank">[Project page]</a>
        <a href="https://github.com/XiaoyuBIE1994/DVAE" target="_blank">[Code]</a>
      </p>
    </div>
  </div>
</article>

