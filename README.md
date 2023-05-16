# CapstoneExtension_MultiClass_SemanticSegmentation

Recommended - Check out my SemanticSegmentation_AbdominalCT repository and its README.md


ABOUT MY CAPSTONE :
Structures in the abdominal region have complex non-geometric overlapping boundaries making it difficult to distinguish and segment them accurately. Low contrast and being surrounded by multiple layers of tissue and organs add to the segmentation difficulty. In this region, we focused on specific abdominal wall muscles which include the left flank, left rectus, right flank, and right rectus.
The abdominal muscles play a crucial role in medical imaging as they provide valuable information for diagnosing abnormalities such as hernias, tumors, and neuro-muscular diseases. Accurate segmentation of these muscles can provide important quantitative information about their size, shape, and location, which can help clinicians make more informed decisions and improve patient outcomes.
The capstone focuses on the automated segmentation of specific abdominal wall muscles. This region of interest was chosen due to the low quantity of research done, difficulty in manual annotation, and application in hernia detection and diagnosis of abdomen wall diseases. The lack of quality publicly available datasets sparked the need to create a novel dataset. This novel dataset was created through careful manual annotations of abdominal CTs and has gone through several ground-truth cheques with professionals.


<img width="1478" alt="Screenshot 2023-05-16 at 2 58 25 PM" src="https://github.com/AnveshSK/CapstoneExtension_MultiClass_SemanticSegmentation/assets/54216044/a41c33fc-e481-4ff2-815d-5a3ccab1493a">


Doing some more literature survey, I proposed 3 extensions - 
1. Multi-class approach
Basically I take each wall as a separate class and extract shared features.
Instead of just getting a effective loss of the abdominal wall muscles as a single entity, they would get it for each muscle group, which would enable them to analyze each group more effectively. Here I continue to use the resized U-Net created for my capstone.
For example - In case of any deformity, surgeons would be able to assess the healing of each muscle group more closely and separately(possible).

2. Backbone and Transfer learning approach
For the capstone we had created a resized U-Net and trained it from scratch. Though it gave us impressive results, a comparative study with other existing U-Net structures like Resnet, VGG, etc. would provide a better view. Using pre-trained weights might result in faster and better training.
How it works? 
U-Net consists of two part : Encoder and Decoder. One extracts the features and the other builds them up to form a mask.
Here a backbone i.e. an existing architecture is used as the encoder part of the U-Net. Basically replace encoder with backbone and leverage its architecture.
You could even use the pre-trained weights for transfer learning. De-coder part is constructed as per encoder

3. Augmentation
In our capstone, I clearly established an improvement in performance is more likely to happen with more data(varied data) rather then improved model architectures.
So following this conclusion, I decided to use data augmentation which allows me to artificially expand data sets to solve the data scarcity issue by leveraging the limited, labeled dataset I already have.
Here Augmentation supports both cases : Small dataset and lack of control of input data.

Combination of extension 1 and 2
I combined my multi-class approach with the backbone approach to try and see if I get any improved results. I had to make similar changes i.e. introduce softmax and number of classes. i did this as some backbone U-Net structures provided better results than the base model.
