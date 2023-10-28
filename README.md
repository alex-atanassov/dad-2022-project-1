# DAD 2022 - Quiz App

First Flutter project for the course **"CS-E4270 - Device-Agnostic Design D"**, held at Aalto University, A.Y. 2022/2023 (Period I).

The project consists in implementing a simple quiz app that fetches topics, questions and answers from a given API, and keeps track of the number of questions answered and correct answers throughout the session.

**Faculty**: Mika P. Nieminen, Arto Hellas

**Deployed online version**: https://alex-atanassov.github.io/dad-2022-project-1/

<div display="inline-block">
<img src="https://github.com/alex-atanassov/dad-2022-project-1/assets/79805163/c6293728-f3f6-49eb-9ad3-69246a24dad1" width=78.7% />
<img src="https://github.com/alex-atanassov/dad-2022-project-1/assets/79805163/2f8df21e-3dc6-415f-87f8-d722a4327594" width=19.5% />
</div>

## Functionality

In this application, the user can answer to quizzes that can concern several topics.<br />The user can select a topic from the **`Home page`**, which fetches the topics from https://dad-quiz-api.deno.dev/topics. This same page will start counting the questions answered and the correct answers, after the first question has been answered.

After choosing a topic, the user is able to answer to the questions from the **`Question page`**, which are fetched randomly among a set of questions inherent to the chosen topic. If the question comes with an image, the page will also display the image beneath the question.<br />From this page, the user can either pick an answer by tapping on one option, or go back to the topics by tapping the button on the bottom; if an answer is picked, the application will send a *POST* request to another API, and then retrieve whether the answer is correct or not.

The **`Answer page`** has the purpose to display the outcome of the answer to the previous question. This page will also display the same counter of questions and correct answers as in the Home page, and two buttons to go back respectively to the Home page, or to the Question page, in which another question of the same topic will be fetched.

The **layout** was implemented taking responsiveness into account. A screen width of 600 represents the threshold for switching between a Mobile layout and a Desktop layout. The biggest difference among the two layouts is the number of columns in which the topics and the question options are displayed, which switches between 1 and 2 columns.<br />In the case of Desktop layout, another aspect of responsiveness is the dynamic resizing of the grid elements and buttons in response to the window sizing; both the grids and the buttons are also constrained by an arbitrary maxWidth value, to make the interface look more compact in fullscreen mode.<br />Also, in the case of the Question page, the grid elements are adjusted in height depending on the number of options, and on whether the question comes with an image to display: this choice was taken with the aim to reduce the scrolling needed to navigate in the application.

### Additional features

The application features an **AppBar** that extends the navigation capabilities across the screens.

The ***back button*** on the top-left corner allows for a quicker navigation from Answer to Question page, and from Question to Home page. These buttons have the same effect as the ElevatedButtons labeled respectively "Show new question" and "Back to topics".

Another improvement to the AppBar is the ***dynamic title***, in the case of the Question page: indeed, while the bars in Home and Answer are statically labeled as "DAD 2022 - Project 1" and "Answer", the Question screen will always bring the same title as the topic chosen from the Home page. For instance, if the user chooses the topic "Basic arithmetics", this title will also be displayed in the following screen.

## Challenges

While the application has been in general straightforward to implement in terms of functionality, there have been a few challenges to solve in order to bring a finished product.

- First, I needed a way to communicate between screens, but there was a case where the usage of Riverpod seemed overkill: I decided to pass the result of the POST Api from the Question to the Answer screen via parameter in the navigation instead, because I would see Riverpod more suitable only if I had to display or update a variable in more points across an application, while here I only needed to pass a boolean (correct/wrong answer) in just one passage. Thus, my challenge was to get more acquainted with the `go_router` package to discover how to achieve this.

- Still related to this use case, it was not trivial to find a suitable place in the code to implement the POST Api followed by the state update. The fact that the state update immediately followed the POST call, and then the new state needed to be displayed in another screen, made it one of the trickiest features of the assignment. I initially attempted to add this method in the Answer page, but after encountering technical difficulties, I realized that moving it to the Question page, and passing the boolean to the other screen, was a more simple solution.

- Another challenge was to design an interface that had a good "look and feel", and that was adaptive to any change to the screen size. This process always involves creativity, but also the skills and patience to make the final outcome look as similar as possible to how it was initially imagined.

## Learning outcomes

- Talking more in general, the biggest learning outcome for me was to get more acquainted with Flutter, a language that I was curious to discover.<br />I have already had past experiences with React Native, a language for Mobile development that serves similar purposes as Flutter, thanks to a Mobile development course that I took last year, where I had to pick one programming language among others (including Flutter). Due to the struggles that I had with React Native, I was recently looking at new opportunities to learn Flutter as well, and now with this course, I have found this opportunity.

- From a more detailed point of view, I would say that this exercise was useful to consolidate what I learned during the past assignments: the key notions required to develop this application successfully were Navigation, API programming, state management and layout building; I got to train myself of these important aspects of Flutter.

- Lastly, another useful aspect that I learned, although not strictly related to Flutter, is how to deploy applications online using Github Pages. In past group projects from other courses, whenever we needed to deploy applications, I always left this task to other colleagues that already had experience with deployment; instead, by working on this project alone, I also got to get my hands on this simple, yet important aspect of Application development.
