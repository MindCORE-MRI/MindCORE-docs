MRI: Stability Scanning
===================================

.. Note::
	Adapted from: John Pyles's protocol described on `MRI Facility QA <https://sites.google.com/view/mri-facility-qa>`_. 

Jump to
-------

* :ref:`overview`
* :ref:`procedure`
* :ref:`references`

----

.. _overview:

Overview
------------

We perform a weekly quality assurance (QA) protocol to monitor the stability of the signal from the Cima.X MRI scanner using the 64-, 32-, and 20-channel head coils and both standard Siemens and CMRR multi-band EPI pulse sequences. The scan protocol is based on the recommendation of John Pyles and colleagues `(Pyles et al, OHBM 2020) <https://sites.google.com/view/mri-facility-qa>`_. Imaging is done on a FUNSTAR (`goldstandardphantoms.com <https://goldstandardphantoms.com/>`_) phantom in the 64- and 32-channel coils using custom 3D-printed phantom holders. Stability is assessed using the Functional Imaging Federated Informatics Research Environment (FBIRN; see `Friedman & Glover, 2006 <https://doi.org/10.1002/jmri.20583>`_) QA metrics, which includes temporal signal to noise ratio (SNR), signal-to-fluctuation noise ratio (SFNR), and mean ghost percentage. The instructions below use a docker-ized version of the FBIRN QA scripts provided by Dr. Chandana Kodiweera of the Dartmouth Brain Imaging Center found `here <https://hub.docker.com/r/diffdocker/fbirnqa>`_.

----

.. _procedure:


Procedure
---------

1. "Register a Patient" with the following parameters. (Note that demographic details are arbitrary, but I like to use biologically plausible sex/height/weight combinations.) Select "Weekly-QA-ses-64ch" as the scan protocol.

[figure of registration screen]

2. Set up the Funstar phantom in the 64-channel coil using the appropriate 3D-printed phantom holder in the bottom/posterior half of the 64-channel coil. Place the phanom with the black plug at the top. I try to center it but it doesn't have to be perfect. Make sure the phantom holder is level as determined by the spirit level. Slide the top/anterior half of the coil into place and plug it in securely. Use the lazer crosshairs to align with the ridges on the anterior/top portion of the coil.

[figure of phantom in 64-ch coil]

.. Note::
    Make sure both top and bottom halves of the 64-channel are in place and plugged in before aligning with the front of the scanner. Do not rely on the scanner's "auto isocenter" feature for this as it will undershoot actual isocenter, resulting in increased ghosting. See `this blog post <https://mindcore.sas.upenn.edu/2025/04/22/ghosting-in-multi-band-epi-scans/>`_ for more information.

 3. Run the anat-localizer scan.
 4. Note the starting temperature of gradient coil #4:
 	a. Navigate to the "System Check" screen from the Home Screen and click on the "Switch User" icon. 

 	[figure of switch user]

 	b. Select "Login with Service Key" and enter the service key from Siemens. See Dr. Kirwan if you don't know where the service key is kept.

 	[figure of login with svc key]

 	c. Select "Diagnosis" > "Magnet & Cooling" > "Gradient & Bore Temp Status". Make a note of the temperature (in C°) for gradient coil 4 (GC4). 

 	[figure of temp screen]

 	d. Leave the System Check window open and navigate back to the "Examination" window by either clicking on it or pressing Alt+Tab.
 5. Confirm the positioning of the first EPI scan. The defailt location is "isocenter", which should be centered on the Funstar phantom. If the phantom is not in isocenter, move the table back to home position and redo the alignment using the lazer crosshairs. You'll need to redo the localizer in that case. 
 6. Turn on all coil elements by clicking on them in the protocol parameters window. Failure to do this will result in lower SNR measures.
 7. 

----

References
----------
Friedman, L., & Glover, G. H. (2006). Report on a multicenter fMRI quality assurance protocol. Journal of Magnetic Resonance Imaging, 23(6), 827–839. `https://doi.org/10.1002/jmri.20583 <https://doi.org/10.1002/jmri.20583>`_ 

Pyles, J., Verstynen, T., Magerkurth, J., Weiskopf, N., Golay, X., & Inglis, B. (2020, June). 2019 MR Facility Quality Assurance: A publicly available protocol. Abstract presented at the Organization for Human Brain Mapping (OHBM) Annual Meeting. `https://www.humanbrainmapping.org/files/2020/OHBM_2020_Virtual_Abstracts_2.pdf <https://www.humanbrainmapping.org/files/2020/OHBM_2020_Virtual_Abstracts_2.pdf>`_ 