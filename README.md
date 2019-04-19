# pecha

Tryout of detect `sentenct region` and `character region` by using `PyTesseract`, `GCP`, `AWS`

## Review

| | PyTesseract | Google Cloud Vision API |	MS Azure Computer Vision API | Amazon Rekognition | 
| :--- | :--- | :--- | :--- | :--- |
| Language |  | 56 languages include Japanese | 26 languages include Japanese	| English ,Number and Symbol | |
| Price | free | （US）	$1.5/1,000 papers（free untill 1,000 papers per a month） | $1.5/1,000 papers（free until 5,000 papers per a month） | $1.0/1,000 papers（free untill 5,000 papers per a month only for first 12 months） |
| confidence | ○ | ○ | ☓	| ○ |
| region of sentence | ○ | ○ | ○ | ○ | 
| region of charactor | ○ | ○ | ☓ | ○ |

* http://cloud.flect.co.jp/entry/2018/06/18/151140


## PyTesseract
> Python-tesseract is a python wrapper for Google's Tesseract-OCR

> Python-tesseract is an optical character recognition (OCR) tool for python. That is, it will recognize and “read” the text embedded in images.

> Python-tesseract is a wrapper for Google’s Tesseract-OCR Engine. It is also useful as a stand-alone invocation script to tesseract, as it can read all image types supported by the Python Imaging Library, including jpeg, png, gif, bmp, tiff, and others, whereas tesseract-ocr by default only supports tiff and bmp. Additionally, if used as a script, Python-tesseract will print the recognized text instead of writing it to a file.

`pytesseract` has `image_to_xxxxx` methods and you can decide type of output by change `xxxxx`.
For example, if you use iamge_to_boxes method, you will get `region of character` below.

> image_to_boxes Returns result containing recognized characters and their box boundaries


```
s 734 494 751 519 0
p 753 486 776 518 0
r 779 494 796 518 0
i 799 494 810 527 0
n 814 494 837 518 0
g 839 485 862 518 0
t 865 492 878 521 0
u 101 453 122 484 0
b 126 453 146 486 0
e 149 452 168 477 0
r 172 453 187 476 0
d 211 451 232 484 0
e 236 451 255 475 0
n 259 452 281 475 0
```

From left, `character`, left bottom point of character box, right top point of character box and page number.
In this case, first line means that character is `s`, left bottom point is [734, 494], right top point is [71, 519] and page numebr is 0.
In conclusion, you can get region of character.

> image_to_data Returns result containing box boundaries, confidences, and other information. Requires Tesseract 3.05+. For more information, please check the Tesseract TSV documentation


This method include below information.

* level: layout information(page, block, paragraph etc...)
* page_num: page number
* block_num: block number
* par_num: paragraph number
* line_num: line number
* word_num: character number
* left, top, width, height: box information of character box
* conf: confidence
* text: character




### Ability

### Speed

### Difficulity of Implementation

Implementation of PyTesseract is very simple and some useful method is prepared in module.

#### Instration

You can use PyTesseract by just pip install.

```
pip install pytesseract
```



If you use macOS, first you shold brew install tesseract.

```
brew install tesseract --HEAD
```


### Source

* https://pypi.org/project/pytesseract/
* http://blog.machine-powers.net/2018/08/06/pytesseract-intro/
* https://pypi.org/project/pytesseract/


## GCP

GCP prepared Vision API including OCR function.
If you use `DOCUMENT_TEXT_DETECTION` as varriable, you can get below list.

* page number
* block number
* paragraph number
* character
* line information
* character position

Example Response:
```
{
  "responses": [
    {
      "textAnnotations": [
        {
          "locale": "en",
          "description": "O Google Cloud Platform\n",
          "boundingPoly": {
            "vertices": [
              {
                "x": 14, "y": 11
              },
              {
                "x": 279, "y": 11
              },
              {
                "x": 279, "y": 37
              },
              {
                "x": 14, "y": 37
              }
            ]
          }
        },
      ],
      "fullTextAnnotation": {
        "pages": [
          {
            "property": {
              "detectedLanguages": [
                {
                  "languageCode": "en",
                  "confidence": 1
                }
              ]
            },
            "width": 281,
            "height": 44,
            "blocks": [
              {
                "property": {
                  "detectedLanguages": [
                    {
                      "languageCode": "en",
                      "confidence": 1
                    }
                  ]
                },
                "boundingBox": {
                  "vertices": [
                    {
                      "x": 14, "y": 11
                    },
                    {
                      "x": 279, "y": 11
                    },
                    {
                      "x": 279, "y": 37
                    },
                    {
                      "x": 14, "y": 37
                    }
                  ]
                },
                "paragraphs": [
                  {
                    "property": {
                      "detectedLanguages": [
                        {
                          "languageCode": "en"
                        }
                      ]
                    },
                    "boundingBox": {
                      "vertices": [
                        {
                          "x": 14, "y": 11
                        },
                        {
                          "x": 279, "y": 11
                        },
                        {
                          "x": 279, "y": 37
                        },
                        {
                          "x": 14, "y": 37
                        }
                      ]
                    },
                    "words": [
                      {
                        "property": {
                          "detectedLanguages": [
                            {
                              "languageCode": "en"
                            }
                          ]
                        },
                        "boundingBox": {
                          "vertices": [
                            {
                              "x": 14, "y": 11
                            },
                            {
                              "x": 23, "y": 11
                            },
                            {
                              "x": 23, "y": 37
                            },
                            {
                              "x": 14, "y": 37
                            }
                          ]
                        },
                        "symbols": [
                          {
                            "property": {
                              "detectedLanguages": [
                                {
                                  "languageCode": "en"
                                }
                              ],
                              "detectedBreak": {
                                "type": "SPACE"
                              }
                            },
                            "boundingBox": {
                              "vertices": [
                                {
                                  "x": 14, "y": 11
                                },
                                {
                                  "x": 23, "y": 11
                                },
                                {
                                  "x": 23, "y": 37
                                },
                                {
                                  "x": 14, "y": 37
                                }
                              ]
                            },
                            "text": "O"
                          }
                        ]
                      },
                    ]
                  }
                ],
                "blockType": "TEXT"
              }
            ]
          }
        ],
        "text": "Google Cloud Platform\n"
      }
    }
  ]
}
```

### Ability

### Speed

### Difficulity of Implementation

#### Instration

Before using Vision API
* Create new GCP Project at GCP
* Activate Cloud Vision API
* Install and initialize Cloud SDK
* Install gcloud component
```
gcloud components update &&
gcloud components install
```
* Prepare enviroment of Node.js




### Source

* https://cloud.google.com/vision/?hl=ja
* https://cloud.google.com/functions/docs/tutorials/ocr?hl=ja
* https://cloud.google.com/vision/docs/ocr

## MS Azure
MS Azure prepared `Computer Vision API`.
MS Asure can detect word level region but charactor level.
Of cource, you can detect text region by using it.


```
{
  "status": "Succeeded",
  "succeeded": true,
  "failed": false,
  "finished": true,
  "recognitionResult": {
    "lines": [
      {
        "boundingBox": [
          125,
          125,
          376,
          95,
          385,
          210,
          147,
          250
        ],
        "text": "Sorry",
        "words": [
          {
            "boundingBox": [
              115,
              125,
              375,
              88,
              393,
              214,
              133,
              251
            ],
            "text": "Sorry"
          }
        ]
      },
      {
        "boundingBox": [
          591,
          170,
          914,
          127,
          926,
          220,
          603,
          263
        ],
        "text": "Have a",
        "words": [
          {
            "boundingBox": [
              586,
              177,
              803,
              147,
              810,
              227,
              601,
              266
            ],
            "text": "Have"
          },
          {
            "boundingBox": [
              838,
              145,
              897,
              142,
              901,
              218,
              844,
              223
            ],
            "text": "a"
          }
        ]
      },
      {
        "boundingBox": [
          208,
          374,
          433,
          376,
          429,
          493,
          203,
          494
        ],
        "text": "Oops!",
        "words": [
          {
            "boundingBox": [
              202,
              373,
              458,
              373,
              458,
              493,
              202,
              493
            ],
            "text": "Oops!"
          }
        ]
      },
      {
        "boundingBox": [
          582,
          248,
          953,
          220,
          962,
          338,
          591,
          367
        ],
        "text": "nice day",
        "words": [
          {
            "boundingBox": [
              578,
              265,
              758,
              239,
              762,
              348,
              579,
              350
            ],
            "text": "nice"
          },
          {
            "boundingBox": [
              780,
              237,
              934,
              221,
              940,
              342,
              784,
              347
            ],
            "text": "day"
          }
        ]
      },
      {
        "boundingBox": [
          164,
          629,
          620,
          600,
          626,
          690,
          169,
          719
        ],
        "text": "See you soon",
        "words": [
          {
            "boundingBox": [
              170,
              628,
              303,
              625,
              309,
              712,
              176,
              716
            ],
            "text": "See"
          },
          {
            "boundingBox": [
              303,
              625,
              435,
              621,
              441,
              701,
              309,
              712
            ],
            "text": "you"
          },
          {
            "boundingBox": [
              447,
              620,
              614,
              613,
              620,
              676,
              453,
              700
            ],
            "text": "soon"
          }
        ]
      },
      {
        "boundingBox": [
          824,
          506,
          1007,
          501,
          1000,
          621,
          837,
          633
        ],
        "text": "bye!",
        "words": [
          {
            "boundingBox": [
              806,
              505,
              1036,
              494,
              1042,
              622,
              812,
              633
            ],
            "text": "bye!"
          }
        ]
      }
    ]
  }
}
```

### Ability

### Speed

### Difficulity of Implementation

### Source
* https://azure.microsoft.com/ja-jp/services/cognitive-services/computer-vision/


## AWS

AWS also has OCR API named `AWS Rekognition`.
You can detect charactor region and text region by AWS Rekognition.

```
{
    "TextDetections": [
        {
            "Confidence": 90.54900360107422,
            "DetectedText": "IT'S",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.10317354649305344,
                    "Left": 0.6677391529083252,
                    "Top": 0.17569075524806976,
                    "Width": 0.15113449096679688
                },
                "Polygon": [
                    {
                        "X": 0.6677391529083252,
                        "Y": 0.17569075524806976
                    },
                    {
                        "X": 0.8188736438751221,
                        "Y": 0.17574213445186615
                    },
                    {
                        "X": 0.8188582062721252,
                        "Y": 0.278915673494339
                    },
                    {
                        "X": 0.6677237153053284,
                        "Y": 0.2788642942905426
                    }
                ]
            },
            "Id": 0,
            "Type": "LINE"
        },
        {
            "Confidence": 59.411651611328125,
            "DetectedText": "I",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.05955825746059418,
                    "Left": 0.2763049304485321,
                    "Top": 0.394121915102005,
                    "Width": 0.026684552431106567
                },
                "Polygon": [
                    {
                        "X": 0.2763049304485321,
                        "Y": 0.394121915102005
                    },
                    {
                        "X": 0.30298948287963867,
                        "Y": 0.3932435214519501
                    },
                    {
                        "X": 0.30385109782218933,
                        "Y": 0.45280176401138306
                    },
                    {
                        "X": 0.27716654539108276,
                        "Y": 0.453680157661438
                    }
                ]
            },
            "Id": 1,
            "Type": "LINE"
        },
        {
            "Confidence": 92.76634979248047,
            "DetectedText": "MONDAY",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.11997425556182861,
                    "Left": 0.5545867085456848,
                    "Top": 0.34920141100883484,
                    "Width": 0.39841532707214355
                },
                "Polygon": [
                    {
                        "X": 0.5545867085456848,
                        "Y": 0.34920141100883484
                    },
                    {
                        "X": 0.9530020356178284,
                        "Y": 0.3471102714538574
                    },
                    {
                        "X": 0.9532787799835205,
                        "Y": 0.46708452701568604
                    },
                    {
                        "X": 0.554863452911377,
                        "Y": 0.46917566657066345
                    }
                ]
            },
            "Id": 2,
            "Type": "LINE"
        },
        {
            "Confidence": 96.7636489868164,
            "DetectedText": "but keep",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.0756164938211441,
                    "Left": 0.634815514087677,
                    "Top": 0.5181083083152771,
                    "Width": 0.20877975225448608
                },
                "Polygon": [
                    {
                        "X": 0.634815514087677,
                        "Y": 0.5181083083152771
                    },
                    {
                        "X": 0.8435952663421631,
                        "Y": 0.52589350938797
                    },
                    {
                        "X": 0.8423560857772827,
                        "Y": 0.6015099883079529
                    },
                    {
                        "X": 0.6335763335227966,
                        "Y": 0.59372478723526
                    }
                ]
            },
            "Id": 3,
            "Type": "LINE"
        },
        {
            "Confidence": 99.47185516357422,
            "DetectedText": "Smiling",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.2814019024372101,
                    "Left": 0.48475268483161926,
                    "Top": 0.6823741793632507,
                    "Width": 0.47539761662483215
                },
                "Polygon": [
                    {
                        "X": 0.48475268483161926,
                        "Y": 0.6823741793632507
                    },
                    {
                        "X": 0.9601503014564514,
                        "Y": 0.587857186794281
                    },
                    {
                        "X": 0.9847385287284851,
                        "Y": 0.8692590594291687
                    },
                    {
                        "X": 0.5093409419059753,
                        "Y": 0.9637760519981384
                    }
                ]
            },
            "Id": 4,
            "Type": "LINE"
        },
        {
            "Confidence": 90.54900360107422,
            "DetectedText": "IT'S",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.10387301445007324,
                    "Left": 0.6685508489608765,
                    "Top": 0.17597118020057678,
                    "Width": 0.14985692501068115
                },
                "Polygon": [
                    {
                        "X": 0.6677391529083252,
                        "Y": 0.17569075524806976
                    },
                    {
                        "X": 0.8188736438751221,
                        "Y": 0.17574213445186615
                    },
                    {
                        "X": 0.8188582062721252,
                        "Y": 0.278915673494339
                    },
                    {
                        "X": 0.6677237153053284,
                        "Y": 0.2788642942905426
                    }
                ]
            },
            "Id": 5,
            "ParentId": 0,
            "Type": "WORD"
        },
        {
            "Confidence": 92.76634979248047,
            "DetectedText": "MONDAY",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.11929994821548462,
                    "Left": 0.5540683269500732,
                    "Top": 0.34858056902885437,
                    "Width": 0.3998897075653076
                },
                "Polygon": [
                    {
                        "X": 0.5545867085456848,
                        "Y": 0.34920141100883484
                    },
                    {
                        "X": 0.9530020356178284,
                        "Y": 0.3471102714538574
                    },
                    {
                        "X": 0.9532787799835205,
                        "Y": 0.46708452701568604
                    },
                    {
                        "X": 0.554863452911377,
                        "Y": 0.46917566657066345
                    }
                ]
            },
            "Id": 7,
            "ParentId": 2,
            "Type": "WORD"
        },
        {
            "Confidence": 59.411651611328125,
            "DetectedText": "I",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.05981886386871338,
                    "Left": 0.2779299318790436,
                    "Top": 0.3935416042804718,
                    "Width": 0.02624112367630005
                },
                "Polygon": [
                    {
                        "X": 0.2763049304485321,
                        "Y": 0.394121915102005
                    },
                    {
                        "X": 0.30298948287963867,
                        "Y": 0.3932435214519501
                    },
                    {
                        "X": 0.30385109782218933,
                        "Y": 0.45280176401138306
                    },
                    {
                        "X": 0.27716654539108276,
                        "Y": 0.453680157661438
                    }
                ]
            },
            "Id": 6,
            "ParentId": 1,
            "Type": "WORD"
        },
        {
            "Confidence": 95.33189392089844,
            "DetectedText": "but",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.06849122047424316,
                    "Left": 0.6350157260894775,
                    "Top": 0.5214487314224243,
                    "Width": 0.08413040637969971
                },
                "Polygon": [
                    {
                        "X": 0.6347596645355225,
                        "Y": 0.5215170383453369
                    },
                    {
                        "X": 0.719483494758606,
                        "Y": 0.5212655067443848
                    },
                    {
                        "X": 0.7195737957954407,
                        "Y": 0.5904868841171265
                    },
                    {
                        "X": 0.6348499655723572,
                        "Y": 0.5907384157180786
                    }
                ]
            },
            "Id": 8,
            "ParentId": 3,
            "Type": "WORD"
        },
        {
            "Confidence": 98.1954116821289,
            "DetectedText": "keep",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.07207882404327393,
                    "Left": 0.7295929789543152,
                    "Top": 0.5265749096870422,
                    "Width": 0.11196041107177734
                },
                "Polygon": [
                    {
                        "X": 0.7290706038475037,
                        "Y": 0.5251666903495789
                    },
                    {
                        "X": 0.842876672744751,
                        "Y": 0.5268880724906921
                    },
                    {
                        "X": 0.8423973917961121,
                        "Y": 0.5989891886711121
                    },
                    {
                        "X": 0.7285913228988647,
                        "Y": 0.5972678065299988
                    }
                ]
            },
            "Id": 9,
            "ParentId": 3,
            "Type": "WORD"
        },
        {
            "Confidence": 99.47185516357422,
            "DetectedText": "Smiling",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.3739858865737915,
                    "Left": 0.48920923471450806,
                    "Top": 0.5900818109512329,
                    "Width": 0.5097314119338989
                },
                "Polygon": [
                    {
                        "X": 0.48475268483161926,
                        "Y": 0.6823741793632507
                    },
                    {
                        "X": 0.9601503014564514,
                        "Y": 0.587857186794281
                    },
                    {
                        "X": 0.9847385287284851,
                        "Y": 0.8692590594291687
                    },
                    {
                        "X": 0.5093409419059753,
                        "Y": 0.9637760519981384
                    }
                ]
            },
            "Id": 10,
            "ParentId": 4,
            "Type": "WORD"
        }
    ]
}
```

### Ability

### Speed

### Difficulity of Implementation

### Source
