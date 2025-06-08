# ML-hw4
Kaggle-ის  Facial Expression Recognition Challenge არის შეჯიბრი,
რომელიც გულისხმობდა 48x48 ნაცრისფერი ფერის სურათების შვიდ ემოციად კლასიფიცირებას.
ექსპერიმენტები რეგისტრირებულია Weights & Biases-ზე (Wandb) და გაშვებულია Google Colab-ში, GitHub-ზე ვერსიის კონტროლით.

ამ შეჯიბრისთვის გამოვიყენე არაერთი მოდელი და მივიღე სხვადასხვა შედეგები და დაკვირვებები.

ჯერ მაქვს simpleCnn:
Goal: 
  გამოიყენება როგორც საბაზისო ტესტი ტრენინგისთვის და აფასებს მოდელის ქცევას მინიმალური სიმძლავრის პირობებში.
  
Architecture:
  2 convolutional layers (Conv → ReLU → MaxPool)
  Flatten → Fully Connected (FC) layer
  Output layer (Softmax)

Characteristics:
  ძალიან ცოტა პარამეტრები
  სწრაფად ატრენინგებს
  Overfits მცირე datasets-ს კარგად

Results:
  წარმატებულად overfits a 20-sample dataset
  უჭირს გენერალიზაცია მთლიან დატაზე
  მნიშვნელოვანია pipeline-ის სისწორის დადასტურებისთვის და საწყისი შეცდომების დებუგინგისთვის

შემდეგ მაქვს betterCnn:
Goal: 
  მოდელის expressiveness-ის გაზრდა და რეგულარიზაციის გაუმჯობესება.
  
Architecture:
  3 convolutional blocks with increasing filters
  ყველა ბლოკი შეიცავს Conv → BatchNorm → ReLU → MaxPool
  Dropout აქვს ყველას FC layer-ის შემდეგ
  Fully Connected layers with more hidden units

რატომაა უკეთესი:
  BatchNorm: ააჩქარებს convergence-ს და ასტაბილურებს training-ს

Dropout: 
  ამცირებს overfitting-ს
More filters and depth: 
  აუმჯობესებს feature extraction

Results:
  კარგად ატრენინგებს როგორც მცირე, ასევე სრულ მონაცემთა დატაზე
  SimpleCNN-თან შედარებით უფრო მაღალი ვალიდაციის სიზუსტე და ნაკლები დანაკარგი
  აჩვენებს სწავლის ძლიერ დინამიკას 

deepCnn:

Goal: 
  გაზარდეთ პრეფორმანსი უფრო ღრმა არქიტექტურის, ოპტიმიზირებული რეგულარიზაციისა და მონაცემთა გაფართოების გამოყენებით.

Architecture:
  4+ convolutional blocks with increasing filters (32 → 64 → 128 → 256)
  Conv → BatchNorm → ReLU → Dropout → MaxPool
  Fully connected layers: 512 → 256 → output
  Dropout rates: 0.3–0.5 depending on the layer

გაუმჯობესებები:
  შეუძლია ისწავლოს უფრო abstract features
  Effective when paired with proper data augmentation
  Benefits from batch normalization in every block

Data Augmentation Used:
  Random horizontal flip
  Random rotation (±10 degrees)
  Random crop with padding

შედეგები:
  Performs საუკეთესოდ მთლიან dataset-ზე
  საუკეთესო validation accuracy და training stability
  სჭირდება დიდი training time და მეტი GPU memory

საბოლოოდ emotionCnn:
Goal:
კიდევ უფრო უკეთესი მოდელი მინდოდა რა.

Architecture:
3 convolutional blocks:
Conv2d(1→64→128→256) → BatchNorm → ReLU → MaxPool → Dropout(0.25–0.5)
Fully Connected: 25666 → 512 → 7 (Softmax via CrossEntropyLoss)

Characteristics:
საშუალოდ კომპლექსური, suitable for Colab GPUs.
BatchNorm stabilizes training; dropout reduces overfitting.
Scalable for deeper architectures.
ჩქარი convergence with Adam optimizer.

Why It’s Effective:
BatchNorm: Accelerates convergence, stabilizes training.
Dropout: Mitigates overfitting.
More filters/depth: Enhances feature extraction.
Data Augmentation: Random horizontal flip, rotation (±10°).

Data Augmentation:
Random horizontal flip (p=0.5)
Random rotation (±10°)
Normalization (mean=0.5, std=0.5)

Results:
Overfits 20-sample dataset (train acc >90%, val acc ~25%).
Full dataset: ~65% validation accuracy, უკეთესია SimpleCNN/BetterCNN.
Stable training, mild overfitting mitigated by dropout and weight decay.
Confusion matrix shows challenges with Sad vs. Neutral.
