# Changelog since v0.3.1
- don't rely on minified variable name for web assets

my teddycloud (0.6.2) build used a variable named `bK` 
- increase specificity of downloadTriggerUrl filter

previous version matched two spots. we just wanne match the assignment, not where it's used as parameter of useState() 
- Dockerfile: Update curl 
- Add another filter 
