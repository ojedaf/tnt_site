
<!-- You can use the [editor on GitHub](https://github.com/ojedaf/tnt_site/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files. -->

Humans use language to guide their learning process [<a id="footnote-1-ref" href="#footnote-1" title="link to footnote">1</a>]. For instance, when teaching how to prepare a cooking recipe, visual samples are often accompanied by detailed or rich language-based instructions (<i>e.g., "Place aubergine onto pan"</i>), which are fine-grained and correlated with the visual content. These instructions are a primary cause of the human ability to quickly learn from few examples because they help to transfer learning among tasks, disambiguate and correct error sources [<a id="footnote-1-ref" href="#footnote-1" title="link to footnote">1</a>]. However, modern deep learning approaches in action recognition~\cite{Jingwei:EtAl:2018,DBLP:TSM, TSN} have mainly focused on a large amount of labeled visual data ignoring the textual descriptions that are usually included along with the videos  \cite{Girdhar2019VideoAT, kinetics}. These limitations have motivated an increasing interest in Few-Shot Learning (FSL) \cite{FSLSurvey}, which consists of learning novel concepts from few labeled instances.

Current approaches in few-shot video classification mostly focus on effectively exploiting the temporal dimension in videos to improve learning under low data regimes. However, most works have largely ignored that videos are often accompanied by rich textual descriptions that can also be an essential source of information to handle few-shot recognition cases. We propose to leverage these human-provided textual descriptions as privileged information when training a few-shot video classification model. Specifically, we formulate a text-based task conditioner to adapt video features to the few-shot learning task. Furthermore, our model follows a transductive setting to improve the task-adaptation ability of the model by using the support textual descriptions and query instances to update a set of class prototypes. Our model achieves state-of-the-art performance on four challenging benchmarks commonly used to evaluate few-shot video action classification models.

![Outline of our FSL setting](/tnt_site/imgs/teaser_fig.png)

## Related Work

### Few-Shot Learning

It is possible to identify two main groups in the FSL literature: (i) gradient-based methods and (ii) metric learning based methods. Gradient-based methods focus on learning a good parameter initialization that facilitates model adaptation by few-shot fine-tuning [<a id="footnote-2-ref" href="#footnote-2" title="link to footnote">2</a>, <a id="footnote-3-ref" href="#footnote-3" title="link to footnote">3</a>, <a id="footnote-4-ref" href="#footnote-4" title="link to footnote">4</a>]. On the other hand, metric-based methods aim to learn or design better metrics for determining similarity of input samples in the semantic embedding space~\cite{koch2015siamese, qi2018low, protoNet, 8578229, vinyals2016matching}. More recently, affine conditional layers are added to the feature extraction backbone in~\cite{BateniSimpleCNAPS,cnapsRequeima} as extension to the conditional neural process framework~\cite{pmlr-v80-garnelo18a} with the goal of effective task-adaptation. In this work, we extend this framework~\cite{pmlr-v80-garnelo18a} differently from~\cite{BateniSimpleCNAPS,cnapsRequeima} by adapting the feature extractor and updating the class representations based on the support textual descriptions and query instances. Our goal is to influence the visual backbone with the structured knowledge captured by pre-trained language models.

## References

<p id="footnote-1">
   1. Gary Lupyan and Benjamin Bergen. <a href="https://onlinelibrary.wiley.com/doi/abs/10.1111/" title="link to footnote">How language programs the mind</a>. volume 70 of Topics in Cognitive Science, 8(2):408–424, 2016. doi: https://doi.org/10.1111/tops.
      <a href="#footnote-1-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-2">
   2. Chelsea Finn, Pieter Abbeel, and Sergey Levine. <a href="http://proceedings.mlr.press/v70/finn17a.html" title="link to footnote">Model-agnostic meta-learning for fast adaptation of deep networks</a>. volume 70 of Proceedings of Machine Learning Research, pages 1126–1135, International Convention Centre, Sydney, Australia, 06–11 Aug 2017. PMLR.
      <a href="#footnote-2-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-3">
   3. Alex Nichol, Joshua Achiam, and John Schulman. <a href="https://arxiv.org/abs/1803.02999" title="link to footnote">On first-order meta-learning algorithms</a>, 2018.
      <a href="#footnote-3-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-4">
   4. Aravind Rajeswaran, Chelsea Finn, Sham M Kakade, and Sergey Levine. <a href="https://proceedings.neurips.cc/paper/2019/file/072b030ba126b2f4b2374f342be9ed44-Paper.pdf" title="link to footnote">Meta-Learning with implicit gradients</a>. In Adv. Neural Inform. Process. Syst., pages 113–124, 2019.
      <a href="#footnote-4-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-5">
   5. J. Ji, S. Buch, JC. Niebles, and A. Soto. <a href="https://openaccess.thecvf.com/content_ECCV_2018/papers/Jingwei_Ji_End-to-End_Joint_Semantic_ECCV_2018_paper.pdf" title="link to footnote">End-to-end joint semantic segmentation of actors and actions in video</a>. In Eur. Conf. Comput. Vis., 2018.
      <a href="#footnote-5-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-6">
   6. Ji Lin, Chuang Gan and Song Han. <a href="https://github.com/mit-han-lab/temporal-shift-module" title="link to footnote">Tsm: Temporal shift module for efficient video understanding</a>. In Int. Conf. Comput. Vis., October 2019.
      <a href="#footnote-6-ref" title="return to text">&#8617;</a> 
</p>

<p id="footnote-7">
<!--    7. Limin Wang, Yuanjun Xiong, Zhe Wang, Yu Qiao, Dahua Lin, Xiaoou Tang, and Luc Van Gool. <a href="https://arxiv.org/abs/1705.02953" title="link to footnote">Temporal segment networks for action recognition in videos</a>. IEEE Trans. Pattern Anal. Mach. Intell., 41(11):2740–2755, 2019.
      <a href="#footnote-7-ref" title="return to text">&#8617;</a> 
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
