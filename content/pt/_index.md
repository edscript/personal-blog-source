---
header:
  - type: typewriter
    methods:
      - typeString: Compartilhar conhecimento...
      - pauseFor: 800
      - deleteAll: false
      - typeString: Foco em unir e ajudar a comunidade!
      - pauseFor: 800
      - deleteChars: 35
      - typeString: <strong>edscript.world</strong>
      - pauseFor: 1000
    options:
      loop: false
      autoStart: false
    height: 280
    paddingX: 100
    align: center
    fontSize: 31
    fontColor: PaleGreen

  - type: text
    height: 200
    paddingX: 50
    paddingY: 0
    align: center
    title:
      - Blog edscript
    subtitle:
      - The world’s fastest framework for building websites
    titleColor:
    titleShadow: true
    titleFontSize: 44
    subtitleColor:
    subtitleCursive: true
    subtitleFontSize: 18
    spaceBetweenTitleSubtitle: 16

  - type: img
    imageSrc: images/header/background.jpg
    imageSize: cover
    imageRepeat: no-repeat
    imagePosition: center
    height: 235
    paddingX: 50
    paddingY: 0
    align: center
    title:
      -
    subtitle:
      -
    titleColor:
    titleShadow: false
    titleFontSize: 44
    subtitleColor:
    subtitleCursive: false
    subtitleFontSize: 16
    spaceBetweenTitleSubtitle: 20

  - type: slide
    height: 235
    options:
        startSlide: 0
        auto: 5000
        draggable: true
        autoRestart: true
        continuous: true
        disableScroll: true
        stopPropagation: true
    slide:
      - paddingX: 50
        paddingY: 0
        align: left
        imageSrc: images/header/background.jpg
        imageSize: cover
        imageRepeat: no-repeat
        imagePosition: center
        title:
          - header title1
        subtitle:
          - header subtitle1
        titleFontSize: 44
        subtitleFontSize: 16
        spaceBetweenTitleSubtitle: 20

      - paddingX: 50
        paddingY: 0
        align: center
        imageSrc: images/header/background.jpg
        imageSize: cover
        imageRepeat: no-repeat
        imagePosition: center
        title:
          - header title2
        subtitle:
          - header subtitle2
        titleFontSize: 44
        subtitleFontSize: 16
        spaceBetweenTitleSubtitle: 20

      - paddingX: 50
        paddingY: 0
        align: right
        imageSrc: images/header/background.jpg
        imageSize: cover
        imageRepeat: no-repeat
        imagePosition: center
        title:
          - header title3
        subtitle:
          - header subtitle3
        titleFontSize: 44
        subtitleFontSize: 16
        spaceBetweenTitleSubtitle: 20
---