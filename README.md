# ImageDiff
## Purpose
ImageDiff determines the differences between two images.

| First input image  | Second input image | Detected differences |
| ------------- | ------------- |------------- |
| <img src="./TestImageDiff/Images/test1a.png" width="200">  | <img src="./TestImageDiff/Images/test1b.png" width="200">  | <img src="./TestImageDiff/Images/test1-result.png" width="200"> |

You can tell it to ignore certain areas in the images. 
Choose some random color, cover up those areas in either of the 
images and supply the RGBA values of the selected color. 

| First input image  | Second input image | Detected differences |
| ------------- | ------------- |------------- |
| <img src="./TestImageDiff/Images/test-ignorecolor-1.png" width="200">  | <img src="./TestImageDiff/Images/test-ignorecolor-2.png" width="200"> |  <img src="./TestImageDiff/Images/test-ignorecolor-result.png" width="200"> |

## Example
```csharp
using Adrichem.ImageDiff;
using Adrichem.ImageDiff.Algorithms;

 var Image1 = new Bitmap(Image.FromFile(Test.Image1));
 var Image2 = new Bitmap(Image.FromFile(Test.Image2));

var Differ = new SimpleDiffer
{
    Options = new DiffOptions
    {
        IgnoreColor = Color.FromArgb(216, 0, 255),
    }
};

//OR

var Differ = new PerceptualDiffer
{
    Options = new PerceptualDiffOptions
    {
        IgnoreColor = Color.FromArgb(255, 216, 0),
        Threshold = 0.1f
    }
};
var DiffOutcome = Differ.Diff(Image1, Image2);
var ActualDiffImage = DiffOutcome.DiffImage;
ActualDiffImage.Save(Path.Combine(Path.GetTempPath(), Test.Name + "diff.png"));

```
