EEG: Avoiding noise in the EEG recording room
===================================

.. Note::
	Page under construction. Please check back later.
	
Overview
------------
The EEG recording room at the MindCORE Neuroimaging Facility is electrically shielded and thus should be very "quiet" in terms of electromagnetic interference, or noise. That said, there are some potential sources of noise in the recording room. Here are some best practices for avoiding noise and getting good, clean data. 

.. Note:: While preprocessing algorithms are now quite advanced at cleaning certain noise from EEG data, there is no substitute for collecting clean data. 

Best Practices
-----------
* Have the subject sit comfortably in the chair with their feet flat on the floor and bottom all the way to the back of the chair. Adjust the chair height so the subject is sitting with knees bent at a comforatable angle. 
* Position the chair away from the monitor and desk such that the subject can comfortably reach the response device (e.g., keyboard) but not so close that the subject is up against the desk.
* **Important:** If you are using desktop speakers to present auditory stimuli or instructions, make sure the speakers are positioned at the *back* of the desk, away from the participant. This type of speaker is a strong source of electromagnetic noise (see video below). If you are not using these speakers for your experiment, turn them off/unplug them.

.. video:: ../images/EEG_noise_sniffing.mov
   :width: 360
   :height: 640
   :autoplay:

*Note*: The video demonstrates the electromagnetic noise emitted by desktop speakers. The instrument depicted is a gaussometer, which is displaying the magnetic field in micro tesla (1 µT = 10 milligaus). According to `this documentation <https://youtu.be/xnwvtR6uVpc?si=CgY-VPddLIPe4NLi>`_, a reasonable noise threshold is 0.4 µT. As you can see in the video, readings next to the speaker are well above this threshold, but the values fall off dramatically with distance (actually with the square of the distance). Conclusion: if your subject is positioned well back from the speakers you should not see appreciable noise from the speakers in your data.