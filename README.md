# ML API
<h3>The workflow of the recommendation system that we created is outlined below.</h3>
<img src='https://drive.google.com/uc?id=1SyhHjvLFoBarDX0g2me5iqkV3B-KDYw0' width="100%"><br>
<img src='https://drive.google.com/uc?id=1Dj0k__gHsvcYCIwJrgQMSafyOdD10968' width="100%">
[Lokergo Flowcharts](https://drive.google.com/file/d/1TDD3FxPrt1yLpuH-R_WcjDbCoGbuIboV/view?usp=sharing). Link to our online flowchart.

- Model A refer to all-MiniLM-L6-v2 and Model B refer to sts-trained-lokergo
- The input shape highlighted in color is performed only once every day after the job data scraping, as a form of computational resource efficiency using a bi-encoder model.
- 'u' and 'v' represent the encoded sentences.
- We combine both the Normalized Cosine Similarity of User Job Preferences and User Skills using a Combiner with the calculation x(weight) + y(weight), where the weight serves as custom weighting between the two Cosine Similarities, with a default value of 0.5.
encoder
<details>
   <summary align="center">More Information</summary>
<p>We utilize all-MiniLM-L6-v2 model as a lightweight bi-encoder without retraining and sts-trained-lokergo model as a retrained cross-encoder using transfer learning from sentence-t5-base model, specifically designed for sentence similarity tasks. Both are employed to calculate user preference similarity with job titles. We use TF-IDF to measure the similarity between user skills and job skills due to its lightweight and fast nature, because its ability to work without requiring dense contextual understanding. We selected model all-MiniLM-L6-v2 for its lightweight design and decent accuracy, while we opted for model sts-trained-lokergo due to its high accuracy, despite its heavier computational requirements. Consequently, we use model sts-trained-lokergo exclusively to compute sentence similarity within the top 100 results obtained from model all-MiniLM-L6-v2. 

For Collaborative Filtering, we employ TF-IDF to calculate similarity in preferences between User A and other users. The highest similarity value indicates significant user similarity. Then, users with similar preferences exchange their content-based recommendations with each other, which are then displayed in the third recommendation section on the website platform. Finally, the algorithm is deployed using Fast API to Google Cloud Run, connected to the backend database.</p>

Three recommendation sections on the website:
1. Content-Based Filtering<br>
   <img src='https://drive.google.com/uc?id=12bTc3tio_TZW0_N3Vf6s3lJdLJMmbyqM' width="600px"><br>
2. Content-Based Filtering + User Location Filter<br>
  <img src='https://drive.google.com/uc?id=1Op8kyoUR9ijcnEwUkYPq58TGs7gf95oU' width="600px"><br>
3. Collaborative Filtering<br>
  <img src='https://drive.google.com/uc?id=14kroWVRD3lz5-thNJ5YIAshQ5qzkSLQe' width="600px"><br>

Future Improvements:
- Increase the number of data sources from other platforms.
- Enhance model performance by expanding the training dataset.
- Modularize the algorithm code for improved scalability.

Reference & Tech stacks
- [HuggingFace STS Model Ranking](https://huggingface.co/spaces/mteb/leaderboard). Link to the similarity task model leaderboard.
- [Difference of Bi-Encoder & Cross-Encoder](https://sbert.net/examples/applications/cross-encoder/README.html). Detailed explaination of bi-encoder and cross-encoder
- [sts-trained-lokergo Model](https://huggingface.co/pahri/sts-trained-lokergo). Our trained model was hosted into HuggingFace repository for easy access

<img src='https://drive.google.com/uc?id=162FIEdB_0e1j_f8RBFs96WW0Ob0mTqx0' width="600px">

C23-VR01 ML Teams.
</details>

