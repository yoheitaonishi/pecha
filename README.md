# pecha

Tryout of detect `sentenct region` and `word region` by using `PyTesseract`, `GCP`, `AWS`

## PyTesseract
> Python-tesseract is a python wrapper for Google's Tesseract-OCR

> Python-tesseract is an optical character recognition (OCR) tool for python. That is, it will recognize and “read” the text embedded in images.

> Python-tesseract is a wrapper for Google’s Tesseract-OCR Engine. It is also useful as a stand-alone invocation script to tesseract, as it can read all image types supported by the Python Imaging Library, including jpeg, png, gif, bmp, tiff, and others, whereas tesseract-ocr by default only supports tiff and bmp. Additionally, if used as a script, Python-tesseract will print the recognized text instead of writing it to a file.



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

#### Region Detect

`pytesseract` has `image_to_xxxxx` methods and you can decide type of output by change `xxxxx`.
For example, if you use iamge_to_boxes method, you will get `region of word` below.

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

From left, `word`, left bottom point of word box, right top point of word box and page number.
In this case, first line means that word is `s`, left bottom point is [734, 494], right top point is [71, 519] and page numebr is 0.
In conclusion, you can get region of word.

> image_to_data Returns result containing box boundaries, confidences, and other information. Requires Tesseract 3.05+. For more information, please check the Tesseract TSV documentation


This method include below information.

* level: layout information(page, block, paragraph etc...)
* page_num: page number
* block_num: block number
* par_num: paragraph number
* line_num: line number
* word_num: word number
* left, top, width, height: box information of word box
* conf: confidence
* text: word


### Source

* https://pypi.org/project/pytesseract/
* http://blog.machine-powers.net/2018/08/06/pytesseract-intro/
* https://pypi.org/project/pytesseract/


## GCP

### Ability

### Speed

### Difficulity of Implementation

GCP prepared Vision API including OCR function.

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

#### Region Detect

If you use `DOCUMENT_TEXT_DETECTION`, you can get below list.

* page number
* block number
* paragraph number
* word
* line information
* word position

Example:
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


### Source

* https://cloud.google.com/vision/?hl=ja
* https://cloud.google.com/functions/docs/tutorials/ocr?hl=ja
* https://cloud.google.com/vision/docs/ocr

## AWS

### Ability

### Speed

### Difficulity of Implementation

