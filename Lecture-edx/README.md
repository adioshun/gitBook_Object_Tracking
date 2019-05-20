# 1. Intorduction 

강의 소개 : 

Hello, and welcome to this course, Multi-object Tracking
for Automotive Systems.
I'm Lennart Svensson, professor of Signal Processing
at Chalmers University of Technology working
with machine learning, Bayesian statistics,
and multi-object tracking.
I'm personally very excited about doing this course
with you first because multi-object tracking
is a topic which is quite challenging to learn
on your own, and second, because the field has
matured significantly over recent years.
I hope that you will find our course an easy way
to obtain a solid understanding of all the main components
in the field.
And I'm Karl Granstrom.
And I'm a researcher and teacher at Chalmers University
of Technology.
And I've been working on different object tracking
problems for about 10 years with a focus on extended object
tracking.
And during this time, I've been part
of many interesting collaborations and projects
where tracking has been applied to data from cameras,
and from LIDARs and radars.
And I think it's a truly fascinating topic.
And I look forward to teaching this course.
As you know, the automotive and transportation sectors
are undergoing a transformation.
Autonomous driving is destined to fundamentally change
the way we think of cars and transportation.
To be safe, autonomous vehicles must
be capable of perceiving their surroundings and all objects
that move around.
In a nutshell, multi-object tracking
is about the accurate perception of the driving environment.
And this is a key enabling technology
for any self-driving vehicle system.
The course is divided into six lectures.
And we will teach three lecturers each.
In the first lecture, we will show some motivational examples
of multi-object tracking applications.
We will define the fundamentals of tracking,
and we will discuss what makes tracking a challenging problem.
Lecture two is about single-object tracking
in clutter.
This is where we learn about the basics of object tracking.
In particular, we learn about standard models
for measurements, when the measurements
may contain both object measurements
and false measurements.
And we study a few simple algorithms for tracking.
In the third lecture, we will learn
about tracking a known number of multiple objects.
And the number of objects is assumed known here
to give a gradual increase in the complexity of the problems
that we face.
So the basic modeling of this problem will be explained,
and we will present some different types of algorithms
for tracking a known number of objects.
In lecture four, we relax the assumption
that the number of objects is known,
and we introduce random finite sets as an elegant tool
to represent uncertainties in both the number of objects
that are present and the states of these objects.
Random finite sets provide us with a unified framework
to model and handle all aspects of multi-object tracking
and have become central to the field of multi-object tracking.
In the fifth lecture, we will finally
arrive where we want to be, and that
is tracking an unknown and time-varying number of objects.
So we will use the random finite set models,
and we'll present and discuss different algorithms
for multiple-object tracking.
And this includes recent advances
like Poisson Multi-Bernoulli Mixture filters,
and delta Generalized Labeled Multi-Bernoulli filters.
Finally in the last lecture, we end
by briefly introducing three topics
that we believe are important for multi-object tracking
in an automotive context, which are deep learning,
sets of trajectories, and extended-object tracking.
As an example, there are a few videos about deep learning,
but rather than teaching you how to do deep
learning, which is beyond the scope of this course,
we highlight the importance of deep learning
in multi-object tracking and discuss the role it
may play in the future.
Please note that this course is a sequel to Sensor Fusion
and Non-linear Filtering for Automotive Systems.
So therefore, unless you already have a solid background
in sensor fusion and non-linear filtering,
we strongly recommend that you first complete that course.
Of course, it's available via edX.
When questions or thoughts pop up about the content,
exercises, or assignments, don't hesitate
to make a post in the discussion forum.
We have seen many times that active participation
in discussions about the material improves the learning.
Again, most welcome to this course.
We look forward to getting to know you.
And good luck with your studies.
