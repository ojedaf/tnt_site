
<!-- You can use the [editor on GitHub](https://github.com/ojedaf/tnt_site/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files. -->

Humans use language to guide their learning process [<a id="footnote-9-ref" href="#footnote-9" title="link to footnote">9</a>]. For instance, when teaching how to prepare a cooking recipe, visual samples are often accompanied by detailed or rich language-based instructions (<i>e.g., "Place aubergine onto pan"</i>), which are fine-grained and correlated with the visual content. These instructions are a primary cause of the human ability to quickly learn from few examples because they help to transfer learning among tasks, disambiguate and correct error sources [<a id="footnote-9-ref" href="#footnote-9" title="link to footnote">9</a>]. However, modern deep learning approaches in action recognition [<a id="footnote-5-ref" href="#footnote-5" title="link to footnote">5</a>, <a id="footnote-8-ref" href="#footnote-8" title="link to footnote">8</a>, <a id="footnote-17-ref" href="#footnote-17" title="link to footnote">17</a>] have mainly focused on a large amount of labeled visual data ignoring the textual descriptions that are usually included along with the videos  [<a id="footnote-4-ref" href="#footnote-4" title="link to footnote">4</a>, <a id="footnote-6-ref" href="#footnote-6" title="link to footnote">6</a>]. These limitations have motivated an increasing interest in Few-Shot Learning (FSL) [<a id="footnote-18-ref" href="#footnote-18" title="link to footnote">18</a>], which consists of learning novel concepts from few labeled instances.

Current approaches in few-shot video classification mostly focus on effectively exploiting the temporal dimension in videos to improve learning under low data regimes. However, most works have largely ignored that videos are often accompanied by rich textual descriptions that can also be an essential source of information to handle few-shot recognition cases. We propose to leverage these human-provided textual descriptions as privileged information when training a few-shot video classification model. Specifically, we formulate a text-based task conditioner to adapt video features to the few-shot learning task. Furthermore, our model follows a transductive setting to improve the task-adaptation ability of the model by using the support textual descriptions and query instances to update a set of class prototypes. Our model achieves state-of-the-art performance on four challenging benchmarks commonly used to evaluate few-shot video action classification models.

![Outline of our FSL setting](/tnt_site/imgs/teaser_fig.png)

## Related Work

### Few-Shot Learning

It is possible to identify two main groups in the FSL literature: (i) gradient-based methods and (ii) metric learning based methods. Gradient-based methods focus on learning a good parameter initialization that facilitates model adaptation by few-shot fine-tuning [<a id="footnote-2-ref" href="#footnote-2" title="link to footnote">2</a>, <a id="footnote-10-ref" href="#footnote-10" title="link to footnote">10</a>, <a id="footnote-12-ref" href="#footnote-12" title="link to footnote">12</a>]. On the other hand, metric-based methods aim to learn or design better metrics for determining similarity of input samples in the semantic embedding space [<a id="footnote-7-ref" href="#footnote-7" title="link to footnote">7</a>, <a id="footnote-11-ref" href="#footnote-11" title="link to footnote">11</a>, <a id="footnote-14-ref" href="#footnote-14" title="link to footnote">14</a>, <a id="footnote-15-ref" href="#footnote-15" title="link to footnote">15</a>, <a id="footnote-16-ref" href="#footnote-16" title="link to footnote">16</a>]. More recently, affine conditional layers are added to the feature extraction backbone in [<a id="footnote-1-ref" href="#footnote-1" title="link to footnote">1</a>, <a id="footnote-13-ref" href="#footnote-13" title="link to footnote">13</a>] as extension to the conditional neural process framework [<a id="footnote-3-ref" href="#footnote-3" title="link to footnote">3</a>] with the goal of effective task-adaptation. In this work, we extend this framework [<a id="footnote-3-ref" href="#footnote-3" title="link to footnote">3</a>] differently from [<a id="footnote-1-ref" href="#footnote-1" title="link to footnote">1</a>, <a id="footnote-13-ref" href="#footnote-13" title="link to footnote">13</a>] by adapting the feature extractor and updating the class representations based on the support textual descriptions and query instances. Our goal is to influence the visual backbone with the structured knowledge captured by pre-trained language models.

### Induction vs Transduction in FSL

Regarding the inference setup, there are two types of approaches: inductive and transductive FSL. We are motivated by recent work following the transductive setting [17, 23, 24, 27], where the unlabeled query data is exploited to further refine the few-shot classifier. For instance, [23] proposes a prototype rectification approach by label propagation. Departing from previous work, our model proposes a novel transductive approach that takes advantage of the support textual descriptions to augment the support videos with the unlabeled instances, leveraging the cross-attention approach.

### Few-Shot Video Classification

There are few works to tackle this problem in video domain. However, most of them are focused only on better exploiting visual or temporal information from videos [3, 19, 26, 42, 44, 45, 47, 48]. Although tackling important aspects in video data modeling, none of the previous works offer solutions to the semantic gap between the few-shot samples and the nuanced and complex concepts needed for video representation learning. We aim to bridge this gap by using textual descriptions as privileged information to contextualize the video feature encoder in conjunction with a classification approach based on class prototypes acting under a transductive inference scheme.

## Our approach

### Problem Definition

FSL aims to obtain a model that can generalize well to novel classes with few support instances. Therefore, we follow the standard FSL setting [33, 39], wherein a trained model f<sub>θ</sub> is evaluated on a significant number of N−way K−shot tasks sampled from a meta-test set D<sub>test</sub>. These tasks consist of N novel categories, from which K samples are sampled to form support set S, where K is a small integer, typically, 1 or 5. The support set S is used as a proxy to classify the B unlabeled instances from the query set Q. The parameters θ of the model f are trained on a meta-training set D<sub>train</sub>, by applying the episodic training strategy [39]. This is, N−way K−shot classification tasks are simulated by sampling from D<sub>train</sub> during meta-training. Q is sampled from the same N categories in such a way that the samples in Q are non-overlapping with S.

### TNT Model

![Our FSL Model](/tnt_site/imgs/full_model_v.png)

#### Task-Conditioned Video Encoder

#### Task Conditioner

![Task Conditioner Module](/tnt_site/imgs/encoder_text.png)

#### Task-Conditioned Transductive Classifier

![Task-Conditioned Transductive Classifier](/tnt_site/imgs/dynamic_module.png)

### Results

<html>
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['bar']});
      google.charts.setOnLoadCallback(drawChart);

      function drawChart() {
        var data = google.visualization.arrayToDataTable([
          ['Task', 'ARN', 'TSN++', 'CMN++', 'TRN++', 'TAM', 'TSN++ Transd', 'TNT'],
          ['EK 1-Shot', 0, 39.10, 0, 0, 0, 42.33, 46.13],
          ['EK 5-Shot', 0, 52.30, 0, 0, 0, 52.66, 59.00],
          ['SS 1-Shot', 0, 33.60, 34.40, 38.60, 42.80, 39.28, 50.44],
          ['SS 5-Shot', 0, 43.00, 43.80, 48.90, 52.30, 52.63, 59.04],
          ['UCF 1-Shot', 62.1, 76.4, 0, 0, 0, 79.23, 86.66],
          ['UCF 5-Shot', 84.8, 88.5, 0, 0, 0, 90.08, 94.14],
          ['Kin 1-Shot', 63.7, 64.5, 65.4, 68.4, 73.0, 68.0, 78.02],
          ['Kin 5-Shot', 82.4, 77.9, 78.8, 82.0, 85.8, 79.87, 84.82]
        ]);

        var options = {
          width: 800,
          chart: {
            title: 'Model Performance',
            subtitle: 'Acc on four challenging video benchmark. EK: EK-92, SS: SS-100, UCF: MetaUCF-101, Kin: Kinetics-100',
          }
        };

        var chart = new google.charts.Bar(document.getElementById('columnchart_material'));

        chart.draw(data, google.charts.Bar.convertOptions(options));
      }
    </script>
  </head>
  <body>
    <div id="columnchart_material" style="width: 800px; height: 500px;"></div>
  </body>
</html>



<html>
<head>
  <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['line']});
      google.charts.setOnLoadCallback(drawChart);

    function drawChart() {

      var data = new google.visualization.DataTable();
      data.addColumn('number', 'Num unlabeled samples in query set');
      data.addColumn('number', 'Transductive');
      data.addColumn('number', 'Inductive');

      data.addRows([
      [5, 53.15999984741211, 54.689998626708984],
      [10, 55.13999938964844, 56.09000015258789],
      [15, 57.439998626708984, 54.849998474121094],
      [20, 58.358360290527344, 55.4354362487793],
      [25, 58.939998626708984, 55.099998474121094],
      [30, 60.18, 56.21],
      [35, 59.588348388671875, 55.56224822998047],
      [40, 58.6418571472168, 55.42253494262695],
      [45, 59.20000076293945, 54.33000183105469],
      [50, 59.4494514465332, 54.76476287841797],
      [55, 59.47999954223633, 54.650001525878906]
      ]);

      var options = {
        chart: {
          title: 'Sensitivity analysis to the number of query set samples.',
          subtitle: 'Model performance on SS-100 in the 5-way, 5-shot task for different B size'
        },
        width: 900,
        height: 500,
        axes: {
          x: {
            0: {side: 'bottom'}
          }
        }
      };

      var chart = new google.charts.Line(document.getElementById('line_top_x'));

      chart.draw(data, google.charts.Line.convertOptions(options));
    }
  </script>
</head>
<body>
  <div id="line_top_x"></div>
</body>
</html>

<html lang="en">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>HTML</title>
<style>
	
	.column {
	  flex: 30%;
	  padding: 5px;
	}
	img {
	  width: 100%;
	}
	.container {
	   display: flex;
	}

	
</style>
</head>  
<body>
    <text style="cursor: default; user-select: none; -webkit-font-smoothing: antialiased; font-family: Roboto; font-size: 16px;" fill="#757575"> Visualization of Class Activation Maps </text>
	<br>
	<text style="cursor: default; user-select: none; -webkit-font-smoothing: antialiased; font-family: Roboto; font-size: 14px;" fill="#BDBDBD"> <strong>Textual action description:</strong> pouring water out of bottle  <br><strong>Action label:</strong> pouring something out of something</text>
	<div class="container">
	   <div class="column">
        <h3 style="cursor: default; user-select: none; -webkit-font-smoothing: antialiased; font-family: Roboto; font-size: 14px; text-align: center; color: #606c71; font-weight: bold;">Video</h3>                                                                            
	     <img src="/tnt_site/imgs/Imagen1.gif" alt="this slowpoke moves" width="250">
	   </div>
	   <div class="column">
    <h3 style="cursor: default; user-select: none; -webkit-font-smoothing: antialiased; font-family: Roboto; font-size: 14px; text-align: center; color: #606c71; font-weight: bold;">w/ Film Layer</h3>
	     <img src="/tnt_site/imgs/Imagen2.gif" alt="this slowpoke moves" width="250">
	   </div>
	   <div class="column">
    <h3 style="cursor: default; user-select: none; -webkit-font-smoothing: antialiased; font-family: Roboto; font-size: 14px; text-align: center; color: #606c71; font-weight: bold;">w/o Film Layer</h3>
	     <img src="/tnt_site/imgs/Imagen3.gif" alt="this slowpoke moves" width="250">
	   </div>
	</div>
</body>
</html> 

<!-- <div class="container">
	   <div class="column">
	     <h3>sample title</h3>
	     <img src="/tnt_site/imgs/Imagen1.gif" alt="this slowpoke moves"  width="250" />
	   </div>
	   <div class="column">
	     <img src="/tnt_site/imgs/Imagen2.gif" alt="this slowpoke moves"  width="250" />
	   </div>
	   <div class="column">
	     <img src="/tnt_site/imgs/Imagen3.gif" alt="this slowpoke moves"  width="250" />
	   </div>
</div> -->


## References

<p id="footnote-1">
   1. Peyman Bateni, Raghav Goyal, Vaden Masrani, Frank Wood, and Leonid Sigal. <a href="https://openaccess.thecvf.com/content_CVPR_2020/papers/Bateni_Improved_Few-Shot_Visual_Classification_CVPR_2020_paper.pdf" title="link to footnote">Improved few-shot visual classification</a>. In IEEE Conf. Comput. Vis. Pattern Recog., June 2020.
      <a href="#footnote-1-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-2">
   2. Chelsea Finn, Pieter Abbeel, and Sergey Levine. <a href="http://proceedings.mlr.press/v70/finn17a.html" title="link to footnote">Model-agnostic meta-learning for fast adaptation of deep networks</a>. volume 70 of Proceedings of Machine Learning Research, pages 1126–1135, International Convention Centre, Sydney, Australia, 06–11 Aug 2017. PMLR.
      <a href="#footnote-2-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-3">
   3. Marta Garnelo, Dan Rosenbaum, Christopher Maddison, Tiago Ramalho, David Saxton, Murray Shanahan, Yee Whye Teh, Danilo Rezende, and S. M. Ali Eslami. <a href="https://arxiv.org/abs/1807.01613" title="link to footnote">Conditional neural processes</a>. In Int. Conf. Machine learning, volume 80, pages 1704–1713. PMLR, 2018.
      <a href="#footnote-3-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-4">
   4. R. Girdhar, J. Carreira, C. Doersch, and A. Zisserman. <a href="https://openaccess.thecvf.com/content_CVPR_2019/papers/Girdhar_Video_Action_Transformer_Network_CVPR_2019_paper.pdf" title="link to footnote">Video action transformer network.</a>. IEEE Conf. Comput. Vis. Pattern Recog., 2019.
      <a href="#footnote-4-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-5">
   5. J. Ji, S. Buch, JC. Niebles, and A. Soto. <a href="https://openaccess.thecvf.com/content_ECCV_2018/papers/Jingwei_Ji_End-to-End_Joint_Semantic_ECCV_2018_paper.pdf" title="link to footnote">End-to-end joint semantic segmentation of actors and actions in video</a>. In Eur. Conf. Comput. Vis., 2018.
      <a href="#footnote-5-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-6">
   6. Will Kay, João Carreira, Karen Simonyan, Brian Zhang, Chloe Hillier, Sudheendra Vijayanarasimhan, Fabio Viola, Tim Green, Trevor Back, Paul Natsev, Mustafa Suleyman, and Andrew Zisserman. <a href="https://arxiv.org/abs/1705.06950" title="link to footnote">The kinetics human action video dataset</a>. CoRR, abs/1705.06950, 2017.
      <a href="#footnote-6-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-7">
   7. Gregory Koch. <a href="https://www.cs.cmu.edu/~rsalakhu/papers/oneshot1.pdf" title="link to footnote">Siamese neural networks for one-shot image recognition</a>. In Int. Conf. Machine learning, 2015.
      <a href="#footnote-7-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-8">
   8. Ji Lin, Chuang Gan and Song Han. <a href="https://github.com/mit-han-lab/temporal-shift-module" title="link to footnote">Tsm: Temporal shift module for efficient video understanding</a>. In Int. Conf. Comput. Vis., October 2019.
      <a href="#footnote-8-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-9">
   9. Gary Lupyan and Benjamin Bergen. <a href="https://onlinelibrary.wiley.com/doi/abs/10.1111/" title="link to footnote">How language programs the mind</a>. volume 70 of Topics in Cognitive Science, 8(2):408–424, 2016. doi: https://doi.org/10.1111/tops.
      <a href="#footnote-9-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-10">
   10. Alex Nichol, Joshua Achiam, and John Schulman. <a href="https://arxiv.org/abs/1803.02999" title="link to footnote">On first-order meta-learning algorithms</a>, 2018.
      <a href="#footnote-10-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-11">
   11. Hang Qi, Matthew Brown, and David G Lowe. <a href="https://arxiv.org/abs/1712.07136" title="link to footnote">Low-shot learning with imprinted weights</a>. In IEEE Conf. Comput. Vis. Pattern Recog., pages 5822–5830, 2018.
      <a href="#footnote-11-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-12">
   12. Aravind Rajeswaran, Chelsea Finn, Sham M Kakade, and Sergey Levine. <a href="https://proceedings.neurips.cc/paper/2019/file/072b030ba126b2f4b2374f342be9ed44-Paper.pdf" title="link to footnote">Meta-Learning with implicit gradients</a>. In Adv. Neural Inform. Process. Syst., pages 113–124, 2019.
      <a href="#footnote-12-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-13">
   13. James Requeima, Jonathan Gordon, John Bronskill, Sebastian Nowozin, and Richard E Turner. <a href="https://arxiv.org/abs/1906.07697" title="link to footnote">Fast and flexible multi-task classification using conditional neural adaptive processes.</a>.  In Adv. Neural Inform. Process. Syst., 2019.
      <a href="#footnote-13-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-14">
   14. Jake Snell, Kevin Swersky, and Richard Zemel. <a href="https://proceedings.neurips.cc/paper/2017/file/cb8da6767461f2812ae4290eac7cbc42-Paper.pdf" title="link to footnote">Prototypical networks for few-shot learning</a>. Adv. Neural Inform. Process. Syst., pages 4077–4087. Curran Associates, Inc., 2017.
      <a href="#footnote-14-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-15">
   15. Flood Sung, Yongxin Yang, Li Zhang, Tao Xiang, Philip H. S. Torr, and Timothy M. Hospedales. <a href="https://arxiv.org/abs/1711.06025" title="link to footnote">Learning to compare: Relation network for few-shot learning</a>.  In IEEE Conf. Comput. Vis. Pattern Recog., pages 1199–1208, 2018. doi: 10.1109/CVPR.2018.00131.
      <a href="#footnote-15-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-16">
   16. Oriol Vinyals, Charles Blundell, Timothy Lillicrap, Daan Wierstra, et al. <a href="https://arxiv.org/abs/1606.04080" title="link to footnote">Matching
networks for one shot learning</a>. In Adv. Neural Inform. Process. Syst., pages 3630–3638, 2016.
      <a href="#footnote-16-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-17">
   17. Limin Wang, Yuanjun Xiong, Zhe Wang, Yu Qiao, Dahua Lin, Xiaoou Tang, and Luc Van Gool. <a href="https://arxiv.org/abs/1705.02953" title="link to footnote">Temporal segment networks for action recognition in videos</a>. IEEE Trans. Pattern Anal. Mach. Intell., 41(11):2740–2755, 2019.
      <a href="#footnote-17-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-18">
   18. Yaqing Wang, Quanming Yao, James T. Kwok, and Lionel M. Ni. <a href="https://dl.acm.org/doi/10.1145/3386252" title="link to footnote">Generalizing from a few examples: A survey on few-shot learning</a>. ACM Comput. Surv., 53(3), June 2020. ISSN 0360-0300. doi: 10.1145/3386252.
      <a href="#footnote-18-ref" title="return to text">&#8617;</a> 
</p>










<!-- Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for
 , .

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

## Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ojedaf/tnt_site/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

## Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
 -->
