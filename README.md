## Installations

```
!pip install tensorflow==1.15.5
!pip install opencv-python==3.4.2.17
!pip install librosa==0.6.0
!pip install numba==0.48
!pip install -qU t5
```
## Clone the code

```
!git clone https://github.com/Mohammadkameel/Talking-Face-Landmarks-from-Speech.git
%cd Talking-Face-Landmarks-from-Speech
!mkdir generated_feature
```

* In this step you should copy and paste Translate.hdf5, TranslateV.hdf5, Range.hdf5 and RangeV.hdf5 to generated_feature folder.

## Training phase (translation part)

```
!python trainTranslation.py -i generated_feature/Translate.hdf5 -ii generated_feature/TranslateV.hdf5  -u 4 -d 40 -c 5 -o Generated_ModelT/
```

## Training phase _ pretrained model (translation part)

you must download D40_C5.h5 model from [here](https://github.com/eeskimez/Talking-Face-Landmarks-from-Speech) and put it in the model folder.

```
!python trainTranslation_pretrained.py -i generated_feature/Translate.hdf5 -ii generated_feature/TranslateV.hdf5  -u 4 -d 40 -c 5 -o Generated_ModelT/
```

* In this step you should copy the generated talkingFaceModelT.h5 from Generated_ModelT/_4/train to models folder.

## Generate control rigs displacements for sample audio (translation part)

```
!python generateTranslation.py -i test_samples/test2.flac -m models/talkingFaceModelT.h5 -d 40 -c 5 -o results/D40_C3_test1
```

## Training phase (range part)

```
!python trainRange.py -i generated_feature/Range.hdf5 -ii generated_feature/RangeV.hdf5 -u 4 -d 40 -c 5 -o Generated_ModelR/
```

## Training phase _ pretrained model (range part)

```
!python trainRange_pretrained.py -i generated_feature/Range.hdf5 -ii generated_feature/RangeV.hdf5 -u 4 -d 40 -c 5 -o Generated_ModelR/
```


* In this step you should copy the generated talkingFaceModelR.h5 from Generated_ModelR/_4/train to models folder

## Generate control rigs displacements for sample audio (range part)

```
!python generateRange.py -i test_samples/test2.flac -m models/talkingFaceModelR.h5 -d 40 -c 5 -o results/D40_C3_test1
```
