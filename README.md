# Week 13 -- Audio (Studio Time) --

Learning Outcomes:

* Familiarity with AudioSource and AudioListener components
* Able to trigger audio using events

## Foreword

This week there is a *brief*, easy practical. Originally, last week was planned to be both Camera & Audio, but we decided to split the two to encourage you to follow the process of creating something new, then incorporating it into your assignment.

As a result, we'd like you to take a step back this week and look at how you can further polish your assignment, while also spending some time exploring various sounds you could use.

Note, your assignment requires you to use the following for sourcing sound **only** - you should not use any other art or audio in your game & any assets should be cited in your report:

* [Kenney.NL](https://kenney.nl/assets): (this site does contain *some* audio assets*
* [Incompetech](https://incompetech.com/music/royalty-free/full_list.php): Contains a library of royalty free music


|   |                                                            Be Mindful of Those Around You                                                            |   |
| --- | :-----------------------------------------------------------------------------------------------------------------------------------------------------: | --- |
|   | You will want headphones for today's lesson. If you do not have any, please turn down the audio on your device (especially if you are using a lab PC). |   |
|   |                                                                                                                                                       |   |

## Adding Looping Audio

Download some music that could be used as generic background music. I'm using the Incompetech site, and found some music that is genuinely quite nice - there's a large list here, so feel free to have a bit of a browse (don't take too long though).

<img src="PracResources\images\01_ListOfMusic.png">

After selecting a music track, the green button allows you to preview the audio, and the blue button allows you to download the audio file (as an mp3). Pretty straightforward.

<img src="PracResources\images\02_MusicPreview.png">

Open up either your assignment or your 2D game from previous weeks if you'd prefer, and create a new folder for our audio files (e.g. `Sounds`). Then, Cut & Paste the music file you just downloaded to your new **Sounds** folder.

From here, the process is the exact same as what we did in the week 3 prac; simply add an `AudioSource` component to an object of your choosing, and attach the sound file.

In the lecture, we covered a few problems that arise during this process as well:

* We need a component that actually picks up any audio played in the scene - an `AudioListener` component. Simply attach this to the camera (ideally your `Main Camera`)
  * You could also attach this to the `Player` if you want, just keep in mind what happens if the player is destroyed
  * There may already be an `AudioListener` component attached to your `Main Camera`. If there is, leave it there.
* We need to attach the music to a permanent object in the scene. Attaching the sound source to the `Main Camera` is a logical idea, but this might be tricky if we want to change music tracks based on triggers (tricky, but not impossible)
* In contrast to our week 3 prac, we actually *do* want to check the field ✅`Play on Awake` when implementing background music since we want our background music to start when our game is played
* Think about whether this sound should be 2D (assumes constant distance) or 3D (changes audio parameters based on distance between source and listener)
  * For background music, we almost always want it to be 2D

Troubleshooting:
If you are stuck, check the week 3 prac. However, there are some common pitfalls we should briefly cover:

* If your music stops playing after a while, check if `Audio Source > ✅Loop` is toggled on or off (we want it to loop for background music, typically)
* If your music never starts, first check if there is *any* audio output, then check if the audio source itself is set to play (`Audio Source >✅Play on Awake`)
  * If it is still not working, you can make a quick script that tests if the current `AudioSource` is playing an audio - note that this should be attached to the object that has the `AudioSource`

<img src="PracResources\images\03_TroubleshootingLogTip.png">

## Reminder - Playtesting

You might have figured this out, but this prac will not take long at all. While you could use the bulk of the remaining lesson time to tweak your game, you may want to use the leftover time to instead start chipping away at the playtesting portion of your assignment. Remember, this is required for your assignment report. As a reminder, here is the brief on playtesting (from the assignment README):

|   | Playtesting |   |
| --- | ------------- | --- |
|   |  When you have completed development of your game, you should invite at least two playtesters (friends, classmates, family, etc) to play your game and give you feedback. You should observe how they play and notice any patterns of play that arise. You should also ask your playtesters about their experience, to see whether you have achieved your design goals. You will be asked to reflect on this in your report. You should use this as an opportunity to genuinely evaluate your work and find areas for improvement. Good critical reflection is better than just saying "It's great!".           |   |
|   |             |   |

Of course, we've included an optional challenge for people who want something a bit more difficult to implement:

## Optional (Easy) Challenge: Event-based Sound Effects

### If You Are Working In The 2D Games Repository

Take a look at the available sound effects on [Kenney.NL](https://kenney.nl/assets), and download some of the sound effects. **If you're using the 2D games practical repository** used in other weeks, follow this implementation for emitting a damage sound every time you take damage:

* Attach an `AudioSource` to your Player
* Navigate to your `Player` script (not `Player_Physics`), and find the code where you take damage
* Add an `AudioSource: Play` node (similar to how we did in Week 3)
* Go back to your `AudioSource`, and give it a sound (ideally one that sounds like a "blip", to reflect that we're taking damage)
* Ensure that `Audio Source > 🔲Loop`  and `Audio Source > 🔲Play on Awake`  are left unticked]

Once you've done this, test that it functions. Again, if you run into trouble, check the troubleshooting steps outlined in the prior section (that sound is on, you have an `AudioListener` in your scene, etc)

### If You Are Working In The Assignment Repository

If you are instead working in your assignment repository, while you may wish to implement the above condition you might also prefer to implement something similar to the following a sound effect that plays:

* Every time your Player 'Jumps'
* Every time you press and hold the the 'Boost' button
* When your player character bonks into a wall/ceiling
* When a timed sequence has been tripped, and a timer is ticking down

## (Optional) Moderate Challenge: Trigger-based Sound Effects

***For this step, it is recommended to look at your week 3/4 project. You may also want to revise the instructions in the week 3 PDF.***

Reflect back to the Week 3 prac, and you'd realise that we've actually already done this optional task. Have a go at recreating the coin pickup, but instead make it something contextually sensible (like a health pick up, or a creaky floorboard tile).

Here's a breakdown of the general "pickup" logic:

1. The object should be triggered by a collision event (using OnTriggerEnter2D)
   * One thing that we should be doing now, which we did not do back then, is check which layer we are colliding with (i.e. check for the Player Layer)
2. The object should perform a sequence of steps if we're proceeding with the logic - it would make sense to start with changing the player's health
3. After which, we want to perform any other "polish" steps, like playing sound
4. At this point, we would want to "disable" our object. However, you may remember we couldn't simply despawn it (like we did in our Week 8 prac) - i.e. if the object is being deleted/despawned, so will the `AudioSource`. How do we resolve this issue?
   * Check the week 3 prac (or your own version of this prac) for a workable solution

Troubleshooting:

* If there is no audio, check if there is an `Audio Listener`, the `Audio Source` has volume turned on, and the **Game** view does not have its sound muted
* If the object is being deleted/despawned, so will the `Audio Source`

## Goodbye & Good Luck

Congratulations, you've completed the last prac! Even though some of these pracs were a bit difficult, I hope you've all enjoyed this series of practicals and have learnt a great deal.

Most importantly, hopefully you've been inspired throughout this semester. I would encourage you all to keep designing/creating outside in your personal time - be it giving your itch.io page some content, or working with teams in a game jam, it is important that you never stop creating.

All the best!

## Completed Tasks

To verify that you've completed all of the content in this prac, check you have done the following:

* Implemented looping audio
* Playtesting, if your game is ready for it

### Show your demonstrator

To show your understanding of this week's content to your prac demonstrator, you may wish to show:

* The audio in your game
  * And where you found the audio
* An implementation of trigger-based audio, if you did that challenge
* How your assignment is progressing
* How your playtesting has gone, if your game is ready for that
