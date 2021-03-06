Title: EVND (Ever Notedown) Notes for Developers





Draft for EVND - Notes for Developers  

&nbsp;


[TOC]

# EVND (Ever Notedown)- Notes for Developers

## Intro to Atom

> **TODO:**
> - [ ] Why Atom?
> - [ ] AppleScript, windows scriptibility
> - [ ] Atom Package developement


## TODO Lists

> **So many...**

### General

- [ ] Write tests (`spec`)
- [ ] Write better documentation

&nbsp;

### Feature Implementations

- [ ] Decide whether to move to [Pagedown](https://code.google.com/p/pagedown/wiki/PageDown)
  - Reasons to use [roaster](https://github.com/gjtorikian/roaster):
    - It's used in the [official Atom Markdown Preview plugin](https://github.com/atom/markdown-preview)
    - Atom/Github people will continue to work on this
  - Reasons to use [pagedown](https://code.google.com/p/pagedown/wiki/PageDown):
    - Used by Stack Overflow / StackEdit
    - More features (e.g. MMD)
- [ ] Diagrams & flowcharts
- [ ] Syncronized scrolling (of editor pane and preview pane)
  - [ ] Ues `diff-match-patch`?
  - [ ] Long text paragraph?
  - [ ] Long lists?
  - [ ] etc.
- [ ] Notes in other formats than Markdown
  - [ ] Plain text
  - [ ] HTML
- [ ] Optional filename/title for fenced code blocks
- [ ] Line numbers for fenced code blocks
- [ ] Shadow DOM (for preview CSS)!
  - _Notes on this:_ blah blah
- [ ] Version control: revert note to a specific commit (GUI in Atom/EVND)
- [ ] Validate `href` of `<a>` elements   
  - (invalid `href`s might cause Evernote sync errors) 
- [ ] Download web images/attachments defined in the document to local file system
- [ ] Grammars
  - Extended GFM:
  - Extended literal Coffee:
    - [ ] Inline math equations!
    - [ ] Attachments
- [ ] Spellcheck? 
  - Currently the spellcheck package won't activate for files of EVND grammar [(code for spellcheck package)](https://github.com/atom/spell-check/blob/master/lib/spell-check-view.coffee)
- [ ] UI
  - [ ] use bootstrap
  - [ ] write sane CSS
- [ ] Use `notification` instead of `window.alert`
- [ ] Use `cson` instead of `json` for the main EVND notes index
- [ ] Different kind of local note storage structure?

&nbsp;

### Progress


#### Spell-check

The Atom core [spell-check](https://atom.io/packages/spell-check) package only activates for specific grammars. Since EVND re-defines grammar for Markdown files when enabled, we'll have to either

- Tell users to add EVND grammar in the `spell-check` settings
- Take advantage of package dependencies in `package.json` and use `atom.config.set` to change settings

&nbsp;

### Bug fixing

- [ ] Syntax highlighting in Atom is still buggy
- [ ] Think of a better way of integrating GIT 
- [ ] HTML->Markdown!
- [ ] `Repository has been destroyed`?
- [ ] Deprecation check?


#### Bug details

##### Number of listeners?
```
(node) warning: possible EventEmitter memory leak detected. 11 data listeners added. Use emitter.setMaxListeners() to increase limit.events.js:232 addListener
```


&nbsp;   
&nbsp;


## Evernote Bugs <i class="icon icon-bug"></i>

### Cannot create notebook with AppleScript - Ticket# 1014193

The examples given on [the official site](https://dev.evernote.com/doc/articles/applescript.php) are not working. More specifically, this  

    tell application "Evernote"
        create notebook "AppleScriptNotebook1"
        create notebook "AppleScriptNotebook2"
        create note title "Note 1" with text "Moving note" notebook "AppleScriptNotebook1"
        move note 1 of notebook "AppleScriptNotebook1" to notebook "AppleScriptNotebook2"
    end tell 

will crash the Evernote client (true as of **vesion 6.0.11**). And this  

    tell application "Evernote"
        set nb1 to make notebook with properties {name:"AppleScriptNotebook1"}
        set name of notebook "AppleScriptNotebook1" to "AppleScriptNotebook2"
    end tell  

produces the following error:  

    error "Evernote got an error: Can’t set notebook \"AppleScriptNotebook1\" to \"AppleScriptNotebook2\"." number -10006 from notebook "AppleScriptNotebook1"

&nbsp;  
&nbsp;

### Random Upload Limit Error - Ticket# 953466

Attempting to update the `HTML content` of a note with basically the same content with get an error message saying

    error "Evernote got an error: Operation would exceed monthly upload allowance.
    
Barring some rare exceptions, users should not see this in EVND...  
&nbsp;  
&nbsp;

