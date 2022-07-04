# filter your photo
#### Video Demo:  <https://youtu.be/mm2eU_yZPrQ>
#### Description:
Hello , World .This is Ram awasthi
i have made this project using html, css, java script, boaotstrap..
i tryed to make as simple , and fast working web app as possible .
my project did,nt use and kind of data base so there is no concern of privarcy
there is lots of filter , and effect..
for example filter brightness,contrast , saturation ,vibrance ..
effects vintage lomo clarity , sin city,cross process ,pinhole ,nostalgia,majesty..
i have all so put remove all filter button to remove all filter that is applied
than final download photo button to download the photo...
.......thanks..cs50 ...
TODO
TRY TO USE MY WEB APP
I have started my cs50 fundamental to Computer Sciences  course  on 1 January 2021
 So I have to say that  this is my first journey  and my first  computer course
  Before this course  I have only used  my PC   for gaming purpose only
   From beginning  I am pretty impressive  by jamesh  but after sometime  course become
     Difficult for me  maybe because  I am not  that good in English
       I have to watch  whole video  again and again  to understand any concept
        But that journey  give me habit  to work hard  and I am very  proud to bea part of cs50
        program  this course is over my expectation
 HOW i got a idea to make photo filter?
         When I have completed  my cs50
         All 10 week   now it's time for  final project
          I am thinking what I have to make and what I will make
             And suddenly   my friend  palak sharma gave me her photo to edit
             to i ask her why you do'nt edit it by your self so she reply her phone have low  specification
              And she is unable to attend
              Then I got an idea  to make   simple and   fast photo editor
               Then I got an idea
                To make
                filter my photo web app
my java script code
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let img = new Image();
let fileName = "";

const downloadBtn = document.getElementById("download-btn");
const uploadFile = document.getElementById("upload-file");
const revertBtn = document.getElementById("revert-btn");

// Filter & Effect Handlers
document.addEventListener("click", (e) => {
  if (e.target.classList.contains("filter-btn")) {
    if (e.target.classList.contains("brightness-add")) {
      Caman("#canvas", img, function () {
        this.brightness(5).render();
      });
    } else if (e.target.classList.contains("brightness-remove")) {
      Caman("#canvas", img, function () {
        this.brightness(-5).render();
      });
    } else if (e.target.classList.contains("contrast-add")) {
      Caman("#canvas", img, function () {
        this.contrast(5).render();
      });
    } else if (e.target.classList.contains("contrast-remove")) {
      Caman("#canvas", img, function () {
        this.contrast(-5).render();
      });
    } else if (e.target.classList.contains("saturation-add")) {
      Caman("#canvas", img, function () {
        this.saturation(5).render();
      });
    } else if (e.target.classList.contains("saturation-remove")) {
      Caman("#canvas", img, function () {
        this.saturation(-5).render();
      });
    } else if (e.target.classList.contains("vibrance-add")) {
      Caman("#canvas", img, function () {
        this.vibrance(5).render();
      });
    } else if (e.target.classList.contains("vibrance-remove")) {
      Caman("#canvas", img, function () {
        this.vibrance(-5).render();
      });
    } else if (e.target.classList.contains("vintage-add")) {
      Caman("#canvas", img, function () {
        this.vintage().render();
      });
    } else if (e.target.classList.contains("lomo-add")) {
      Caman("#canvas", img, function () {
        this.lomo().render();
      });
    } else if (e.target.classList.contains("clarity-add")) {
      Caman("#canvas", img, function () {
        this.clarity().render();
      });
    } else if (e.target.classList.contains("sincity-add")) {
      Caman("#canvas", img, function () {
        this.sinCity().render();
      });
    } else if (e.target.classList.contains("crossprocess-add")) {
      Caman("#canvas", img, function () {
        this.crossProcess().render();
      });
    } else if (e.target.classList.contains("pinhole-add")) {
      Caman("#canvas", img, function () {
        this.pinhole().render();
      });
    } else if (e.target.classList.contains("nostalgia-add")) {
      Caman("#canvas", img, function () {
        this.nostalgia().render();
      });
    } else if (e.target.classList.contains("hermajesty-add")) {
      Caman("#canvas", img, function () {
        this.herMajesty().render();
      });
    }
  }
});

// Revert Filters
revertBtn.addEventListener("click", (e) => {
  Caman("#canvas", img, function () {
    this.revert();
  });
});

// Upload File
uploadFile.addEventListener("change", () => {
  // Get File
  const file = document.getElementById("upload-file").files[0];
  // Init FileReader API
  const reader = new FileReader();

  // Check for file
  if (file) {
    // Set file name
    fileName = file.name;
    // Read data as URL
    reader.readAsDataURL(file);
  }

  // Add image to canvas
  reader.addEventListener(
    "load",
    () => {
      // Create image
      img = new Image();
      // Set image src
      img.src = reader.result;
      // On image load add to canvas
      img.onload = function () {
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0, img.width, img.height);
        canvas.removeAttribute("data-caman-id");
      };
    },
    false
  );
});

// Download Event
downloadBtn.addEventListener("click", () => {
  // Get ext
  const fileExtension = fileName.slice(-4);

  // Init new filename
  let newFilename;

  // Check image type
  if (fileExtension === ".jpg" || fileExtension === ".png") {
    // new filename
    newFilename = fileName.substring(0, fileName.length - 4) + "-edited.jpg";
  }

  // Call download
  download(canvas, newFilename);
});

// Download
function download(canvas, filename) {
  // Init event
  let e;
  // Create link
  const link = document.createElement("a");

  // Set props
  link.download = filename;
  link.href = canvas.toDataURL("image/jpeg", 0.8);
  // New mouse event
  e = new MouseEvent("click");
  // Dispatch event
  link.dispatchEvent(e);
}