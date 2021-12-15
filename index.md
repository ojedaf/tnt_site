
<!-- You can use the [editor on GitHub](https://github.com/ojedaf/tnt_site/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files. -->

Current approaches in few-shot video classification mostly focus on effectively exploiting the temporal dimension in videos to improve learning under low data regimes. However, most works have largely ignored that videos are often accompanied by rich textual descriptions that can also be an essential source of information to handle few-shot recognition cases. We propose to leverage these human-provided textual descriptions as privileged information when training a few-shot video classification model. Specifically, we formulate a text-based task conditioner to adapt video features to the few-shot learning task. Furthermore, our model follows a transductive setting to improve the task-adaptation ability of the model by using the support textual descriptions and query instances to update a set of class prototypes. Our model achieves state-of-the-art performance on four challenging benchmarks commonly used to evaluate few-shot video action classification models.

![Outline of our FSL setting](/tnt_site/imgs/teaser_fig.png)

## Related Work

### Few-Shot Learning

It is possible to identify two main groups in the FSL literature: (i) gradient-based methods and (ii) metric learning based methods. Gradient-based methods focus on learning a good parameter initialization that facilitates model adaptation by few-shot fine-tuning \cite{pmlr-v70-finn17a,nichol2018firstorder,rajeswaran2019meta}. On the other hand, metric-based methods aim to learn or design better metrics for determining similarity of input samples in the semantic embedding space~\cite{koch2015siamese, qi2018low, protoNet, 8578229, vinyals2016matching}. More recently, affine conditional layers are added to the feature extraction backbone in~\cite{BateniSimpleCNAPS,cnapsRequeima} as extension to the conditional neural process framework~\cite{pmlr-v80-garnelo18a} with the goal of effective task-adaptation. In this work, we extend this framework~\cite{pmlr-v80-garnelo18a} differently from~\cite{BateniSimpleCNAPS,cnapsRequeima} by adapting the feature extractor and updating the class representations based on the support textual descriptions and query instances. Our goal is to influence the visual backbone with the structured knowledge captured by pre-trained language models.

<!-- Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

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
