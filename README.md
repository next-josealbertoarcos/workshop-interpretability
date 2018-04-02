# Machine learning interpretability

Machine learning has a huge potential to improve products, processes and research. But machines usually don’t give an explanation for their predictions, which hurts trust and creates a barrier for the adoption of machine learning. This PoC is about making machine learning models and their decisions interpretable.

The main theoretical resource in which this PoC is based in the great [Interpretable Machine Learning Book](https://christophm.github.io/interpretable-ml-book/).


# Resources

You can find the slides of the workshop [here](https://docs.google.com/presentation/d/19KTzk0uSAs6b3Brud-e_TYJiZbPncsiXMG-eXMXM1U4/edit?usp=sharing).

Several interpretability methods have been tried. You can find examples in R and Python notebooks in each folder.

In order to be able to make a fair comparison between methods, the same model has been explained with all of them. The model is a XGBoost model trying to predict if a passenger will die or survive in the Titanic dataset. You can find the way the model was created in the folder *0-model-to-explain*.

Partial Dependence Plots (PDPs) and Individual Conditional Expectations (ICEs) are extremelly simple and useful tools to show what a model is doing. You will find some interesting examples and ways to use them in the folders *1-partial-dependence-plots* and *2-individual-conditional-expectation*.

Permutation Feature Importance lets us estimate the global importance of each feature in a model. And we can apply this to any model! It is a great way to get a glance of what features the model is using to take decisions. Some examples can be found in *3-permutation-feature-importance*.

LIME is a nice method to interpret any model, but it is a bit unstable. I recommend using it to interpret models when working with images, as it is the only working implementation right now able to work with images. Some examples (tabular data) and the explanation of its unstability can be found in *4-lime*.

XGBoost Explainer is just great. It lets you explain any prediction done by a XGBoost model in terms of the values of all the input features. There is also a version to use with Random Forest models. You will find examples and more info in the *5-xgboost-explainer* folder.

Relating XGBoost Explainer and LIME, SHAP claims to be "the best" method to explain particular predictions. In fact, it is already implemented inside XGBoost. Its results are similar to those methods, but they should keep a deeper coherence, and are based on game theory. Some examples may be found in *7-shap*.

Last but not least, there are some methods to map predictions to training set samples. This is great! We not only know why the model is predicting something, but we know which samples in the training set are influencing this decision. So we can clean the training set if something goes wrong. A brute-force example of this method can be found in *6-leave-one-out-retraining*.

And that's it!! I recommend reading the great [Interpretable Machine Learning Book](https://christophm.github.io/interpretable-ml-book/), which is updated every week with new methods and resources.


# Docker images

I have prepared a docker image so that you are able to execute all the notebooks without the dependency problem. You can build the image using the included docker file.

In order to build the image:
```
sudo docker build --tag interpretability:v0 .   
```


To execute the Python version (Jupyter & Co):

```
sudo docker run --net="host" -v /home/josearcos/workshop-interpretability/:/usr/local/notebooks interpretability:v0
```

To execute the R version (RStudio Server with every package you will need):

``` 
sudo docker run --net="host" -v /home/josearcos/workshop-interpretability/:/home/rstudio/notebooks interpretability:v0 /init
```

When running the container, remember to share the folder containing all the notebooks (in the example, my path was */home/josearcos/workshop-interpretability/*).

To connect to RStudio Server, just go to:   
http://localhost:8787/   
And enter with:   
user = rstudio   
pass = rstudio  

To connect to Jupyter notebook, just follow the URL shown in the console.
