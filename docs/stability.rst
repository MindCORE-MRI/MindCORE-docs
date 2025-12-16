Scanner Stability Measures
==========================

.. image:: images/64-Ch_summary.png
   :alt: 64-channel head coil summary
   :width: 100%

.. image:: images/32-Ch_summary.png
   :alt: 32-channel head coil summary
   :width: 100%

.. image:: images/20-Ch_summary.png
   :alt: 20-channel head coil summary
   :width: 100%

Click on any image above to see a larger version.

**Methods** Above are the results of the weekly quality assurance (QA) protocol in which we assess the stability of the fMRI signal from the Cima.X scanner using the 64-, 32-, and 20-channel head coils and both standard Siemens and CMRR multi-band EPI pulse sequences (denoted "Siemens" and "CMRR" in the figures above). The scan protocol is based on the recommendation of John Pyles and colleagues (Pyles et al, OHBM 2020) found here: `https://sites.google.com/view/mri-facility-qa <https://sites.google.com/view/mri-facility-qa>`_. Scan parameters are typical of research protocols for TR, TE, and resolution. All scans in the plots above are in straight axial orientation unless specified as AC-PC aligned. Imaging is done on a `FUNSTAR phantom <https://goldstandardphantoms.com/products/funstar/>`_ in the 64- and 32-channel coils using custom 3D-printed phantom holders. Stability is assessed using the Functional Imaging Federated Informatics Research Environment (FBIRN; see Friedman & Glover, 2006) QA metrics, which includes temporal signal to noise ratio (SNR), signal-to-fluctuation noise ratio (SFNR), and mean ghost percentage. QA metrics are assessed using a docker-ized version of the FBIRN QA scripts provided by Dr. Chandana Kodiweera of the Dartmouth Brain Imaging Center found here: `https://hub.docker.com/r/diffdocker/fbirnqa <https://hub.docker.com/r/diffdocker/fbirnqa>`_.

For more on the weekly QA protocol, see this `blog post <https://mindcore.sas.upenn.edu/2025/04/08/mri-stability-scanning/>`_.