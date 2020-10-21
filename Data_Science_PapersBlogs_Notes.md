## Trivago:

#### Machine Learning and Bathtubs - How Small Visual Changes Improve User Experience" 
	
- Link: https://tech.trivago.com/2019/08/21/machine-learning-and-bathtubs-how-small-visual-changes-improve-user-experience/	
- Description: The idea is to adjust the main images of hotels to reflect the user intent coming from SEM ads containing spa concepts (concept-based main images)
- Technologies: AWS stack for pipelines, RNN, CNN with transfer learning. 
- More: Automated (with CV) image labeling of Trivago 100+ millions active images for Spa & Wellness. For training some public data has been used along with existing handpicked image tags from our trivago hoteliers. A questionnaires have been prepared based on Amazon Mechanical Turk to align the images semantically. The resulting dataset had 2,000 images for each of the categories of "Sauna", "Pool", "Gym", "Yoga", "Hot-tub" and "Massage". Five different CNN architectures (InceptionV3, VGG16, Xception, ResNet50, InceptionResnetV2) were evaluated with VGG16 chosen as final model. Precision was used as evaluation metric (to min False Positives). To deal with the images that had to be negated (out all classes that are beyond this concept) two additional (unbalanced) classes were introduced "Bedroom" and "Non-Spa". An average  Precision and Recall  of ~85% and ~89% for the individual Spa & Wellness classes.
