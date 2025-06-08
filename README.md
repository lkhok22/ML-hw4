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
