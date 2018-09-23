# uwss-website

## To get up and running:
1. Install a ruby development environment. See https://jekyllrb.com/docs/installation/.
2. Install Jekyll using: `gem install jekyll bundler` at the command line.
3. Clone the git repo to your computer: `git clone https:git@github.com/tpreynolds/uwss-website uwss-website`. I'd suggest putting this in your home directory.
4. cd into the directory `uwss-website` that you just created.
5. Run the command `bundle exec jekyll serve` at the command line.
6. In a web browser, go to `http://localhost:4000` to see the website.

## Folder Structure
 - Images are saved in /images/
 - All markdown files for the website pages are in the `/_posts/` folder. 
 - All styling, colouring, boxes, icons and whatever are defined in the `css/style.css` file. 
 - Don't touch anyhting in the `/_site/` folder.

## Other stuff 
Themes:
 - Based on Twenty by HTML5 UP (n33.co @n33co dribbble.com/n33)

Video Walkthroughs:
 - https://jekyllrb.com/tutorials/video-walkthroughs/ 

Other:
 - I've found that I need to run the command `eval “$(rbenv init -)”` before running `jekyll serve` to get the website up and running. 
 - homepage for jekyll: https://jekyllrb.com/ 
 - Always save posts with `YYYY-MM-DD-title.markdown` format.
 - DO NOT run jekyll serve from inside any sub-folder — must be in the ROOT.
 - Icons come from: Font Awesome (fortawesome.github.com/Font-Awesome)
