## Inspiration
In 2020, we were forced to take our hackathon online because of the pandemic. When that happened, we started brainstorming how we could run the hackathon online and do everything that we wanted to virtually. One of those things was a team formation event that we do for solo hackers who want to find a team. Someone jokingly brought up that it would be funny if we had a Tinder for hackers. And we all laughed.

## What it does 
Lattice is a Tinder for hackers. It is an app where hackathon participants can create a profile, which includes their skills, project ideas, and skills they are looking for in potential teammates. Once you create a profile, you can see the profiles of other hackers and swipe either left or right. If two hackers both swipe right on each other, they both get a notification about the match, along with contact details for each other.

The browse feature is powered by a recommendation engine that compares two profiles. The profiles are likely to match if one person has the skills the other person needs, and vice versa. It is a very fast way to find the potential teammates that you most need.

## Implementation, Challenges, Learnings

### Swipe
The most important part of Lattice is the Tinder-like swiping UI and animation. So I started working on that first. There are 3 different parts of that UI - the animation of the cards first "falling" into view, the touch gesture we make on the screen when swiping, and the card following that gesture and swiping out of view. The animations were done using React-Spring, a library that changes values over time along a curve, and these changing values can be used to change the size or position of an element on screen which makes it appear like it's moving.

### Browse
The next important part was the backend, specifically the recomendation algorithm. I was only using the skills defined in the profiles to predict matches, but wanted to keep it open to expansion in the future, so the algorithm is decoupled from the rest of the backend so that it can be developed on easily.

### Chat
I thought a lot about whether I should build in a chat feature, and I decided against it. Chat is very complex, and we are already using Discord for the hackathon. A discord integration was considered but I went for the much simpler solution of hackers putting their discord username in the profile. This would be shown to other hackers only once they match. However there are a lot of fun ideas that could be built on top of the discord integration.

### Notifications
I did not want to build a native mobile application, since I had much more experience with web apps. So I decided to make Lattice a Progressive Web App (PWA), which means it would run a service worker in the background that can subscribe to push events and show notifications on the hacker's phone or PC. Figuring out push notifications was a very fun and informative journey, it took me everywhere between service worker registration, web-push api and architecture, creating device notifications and actions, and managing multiple devices for the same user.

### Auth
Implementing auth from scratch is not something I'd recommend most people do (unless for educational purposes). Lattice uses a simple JWT token-based auth, which is challenging to implement while keeping it extensible. Ideally I might remove the entire auth implementation and plug in a cloud auth service like Clerk or Firebase.

### Integration
One tricky part was the integration of auth with our registration system - we made Lattice integrated with our hackathon's system, so any running version of Lattice can only be used for a specific hackathon. This also allowed us to customize it every year with the hackathon's custom branding and make it feel integrated into the hackathon experience.

## What's next for Lattice

Since building the initial version, Lattice has been used for atleast 6 hackathons, including the hybrid and in-person ones, just because both our organizers and hackers loved using it. Lattice can very easily be deployed as an independent application that is not tied to one hackathon, and acts as a generalized matching app for hackers. The profile can then be expanded to include the hackathons you are attending, so that you can also filter for hackers that are also attending to those hackathons. It can potentially be integrated into Devpost as well, so that hackers don't have to create a new profile.

Expanding what is included in the profile is an important step in the evolution of Lattice. More information about hackers means they will have an easier time expressing what they want and finding what they are looking for. It also allows us to empower the recommendation engine even more. The recommendation engine can also be expanded with machine learning capabilities if enough hackers end up using Lattice.

Finally, Lattice is not only a hacker matching tool, it can be used for so much more. It can be promoted as a much more generalized networking and social collaboration tool, especially within a hackathon or conference or any tech event. You can use it to find other hackers, mentors, organizers, sponsors, speakers, or anyone else at the hackathon. If you are a solo hacker, you can still use Lattice to find mentors or organizers who might be able to help you. Hackers looking for a job can connect with sponsor reps who are looking to hire, or other students that work at those companies looking to chat.

The power of Lattice lies in discovering people who are going to be in an event with you. This discovery has unlimited potential for collaboration and networking.
