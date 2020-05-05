# Handwritten Text Recognition (OCR) with MXNet Gluon 
handwritten text recognition with mxnet and gluon. Thanks to https://pythonawesome.com/handwritten-text-recognition-ocr-with-mxnet-gluon/
These notebooks have been created by [Jonathan Chung](https://github.com/jonomon), as part of his internship as Applied Scientist @ Amazon AI, in collaboration with [Thomas Delteil](https://github.com/ThomasDelteil) who built the original prototype.
## Usage
Parameters:
        image: input image that includes handwritten text
        form_size: possible form size
        device: device that module running on.
        num_device: number of device that module running on.
        crop: cropping detected text area
        ScliteHelperPATH: Tool that helps to get quantitative results. https://github.com/usnistgov/SCTK
        show: Show plot if show=True. default; show=False
handwritten_text_recognization Usage: 
    htr = handwritten_text_recognization()
    htr()

handwritten_text_recognization Usage:
    htr_test = handwritten_text_recognization_test(image_name="elyaz2.jpeg", filter_number=1, form_size=(1120, 800), device=None, show=True)
    htr_test()
    
## Requirements:
    scikit_image
    scipy
    matplotlib
    tqdm
    mxnet_cu102mkl
    pandas
    nltk
    mxboard
    numpy
    gluonnlp
    leven
    ipython
    mxnet
    mxboard
    Pillow
    pyenchant
    scikit-image
    sympound
    weighted_levenshtein
    hnswlib
    pdoc3
    pybind11
    setuptools
    """

## Setup

`git clone https://github.com/develooper1994/handwritten-text-recognition --recursive`

You need to install SCLITE for WER evaluation
You can follow the following bash script from this folder:

```bash or batch
cd ..
git clone https://github.com/usnistgov/SCTK
cd SCTK
export CXXFLAGS="-std=c++11" && make config
make all
make check
make install
make doc
cd -
```

You also need hsnwlib

```bash or batch
pip install pybind11 numpy setuptools
pip install hnswlib
```

## Overview 

![](https://cdn-images-1.medium.com/max/1000/1*nJ-ePgwhOjOhFH3lJuSuFA.png)

The pipeline is composed of 3 steps:
- Detecting the handwritten area in a form [[blog post](https://medium.com/apache-mxnet/page-segmentation-with-gluon-dcb4e5955e2)], [[jupyter notebook](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/1_b_paragraph_segmentation_dcnn.ipynb)], [[python script](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/ocr/scripts/paragraph_segmentation_dcnn.py)]
- Detecting lines of handwritten texts [[blog post](https://medium.com/apache-mxnet/handwriting-ocr-line-segmentation-with-gluon-7af419f3a3d8)], [[jupyter notebook](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/2_line_word_segmentation.ipynb)], [[python script](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/word_and_line_segmentation.py)]
- Recognising characters and applying a language model to correct errors. [[blog post](https://medium.com/apache-mxnet/handwriting-ocr-handwriting-recognition-and-language-modeling-with-mxnet-gluon-4c7165788c67)], [[jupyter notebook](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/3_handwriting_recognition.ipynb)], [[python script](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/ocr/scripts/handwriting_line_recognition.py)]

The entire inference pipeline can be found in this [notebook](https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet/blob/master/0_handwriting_ocr.ipynb). See the *pretrained models* section for the pretrained models.

A recorded talk detailing the approach is available on youtube. [[video](https://www.youtube.com/watch?v=xDcOdif4lj0)]

The corresponding slides are available on slideshare. [[slides](https://www.slideshare.net/apachemxnet/ocr-with-mxnet-gluon)]

## Pretrained models:

You can get the models by running `python get_models.py`:

## Sample results

![](https://cdn-images-1.medium.com/max/2000/1*8lnqqlqomgdGshJB12dW1Q.png)

The greedy, lexicon search, and beam search outputs present similar and reasonable predictions for the selected examples. In Figure 6, interesting examples are presented. The first line of Figure 6 show cases where the lexicon search algorithm provided fixes that corrected the words. In the top example, “tovely” (as it was written) was corrected “lovely” and “woved” was corrected to “waved”. In addition, the beam search output corrected “a” into “all”, however it missed a space between “lovely” and “things”. In the second example, “selt” was converted to “salt” with the lexicon search output. However, “selt” was erroneously converted to “self” in the beam search output. Therefore, in this example, beam search performed worse. In the third example, none of the three methods significantly provided comprehensible results. Finally, in the forth example, the lexicon search algorithm incorrectly converted “forhim” into “forum”, however the beam search algorithm correctly identified “for him”.

## Dataset:
* To use test_iam_dataset.ipynb, create credentials.json using credentials.json.example and editing the appropriate field. The username and password can be obtained from http://www.fki.inf.unibe.ch/DBs/iamDB/iLogin/index.php.

* **It is recommended to use an instance with 32GB+ RAM and 100GB disk size, a GPU is also recommended. A p3.2xlarge would be the recommended starter instance on AWS for this project**

## Appendix

### 1) Handwritten area

#####  Model architecture

![](https://cdn-images-1.medium.com/max/1000/1*AggJmOXhjSySPf_4rPk4FA.png)

##### Results

![](https://cdn-images-1.medium.com/max/800/1*HEb82jJp93I0EFgYlJhfAw.png) 

### 2) Line Detection

##### Model architecture

![](https://cdn-images-1.medium.com/max/800/1*jMkO7hy-1f0ZFHT3S2iH0Q.png)

##### Results

![](https://cdn-images-1.medium.com/max/1000/1*JJGwLXJL-bV7zsfrfw84ew.png)

### 3) Handwritten text recognition

##### Model architecture

![](https://cdn-images-1.medium.com/max/800/1*JTbCUnKgAySN--zJqzqy0Q.png)

##### Results

![](https://cdn-images-1.medium.com/max/2000/1*8lnqqlqomgdGshJB12dW1Q.png)

##### Requirement
At leats 11GB VRAM GPU or 11GB space on RAM.

### Thanks to
https://pythonawesome.com/handwritten-text-recognition-ocr-with-mxnet-gluon/
https://www.youtube.com/watch?v=xDcOdif4lj0&t=1281s
https://github.com/awslabs/handwritten-text-recognition-for-apache-mxnet