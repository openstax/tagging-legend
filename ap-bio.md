# To Do

- Phil to add grammar.

# Overview

- [Conventions](#conventions)
- [CNXML Templates](#templates)
- [Full Tag List](#full-tag-list)
  - [Tutor-specific](#tutor-specific)
  - [CNX-specific](#cnx-specific)
- [Full Grammar](#full-grammar)

# Conventions

- `os-*`: OST and CNX care about
  - `os-teacher`: Teacher Edition content
  - `os-exercise`: Exercise to pull from exercises
  - `os-embed`: URL to use to pull exercises and videos that should be embedded in the content. No simulations expected in AP Bio.
- `ost-*`: Only OST cares about
  - `ost-tag-*`
    - `ost-tag-lo-apbio-*`: ie `ost-tag-lo-apbio-ch12-s01-lo04` use these to identify Program LO's
    - `ost-tag-std-apbio-*`: ie `ost-tag-std-apbio-4` use these to identify Big Ideas
    - `ost-tag-std-apbio-*-*`ie `ost-tag-std-apbio-4-a` use these to identify Enduring Understanding
    - `ost-tag-std-apbio-*-*-*-*`ie `ost-tag-std-apbio-4-a-3-a` use these to identify Essential Knowledge
    - `ost-tag-std-apbio-lo-*-`ie `ost-tag-std-apbio-lo-2-10` use these to identify AP Learning Objectives
    - `ost-tag-std-apbio-sciprac-*-*`ie `ost-tag-std-apbio-sciprac-4-2` use these to identify Science Practices
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : Not on any features at the moment. 
  - `ost-feature` : This is a non-assessed feature that should be a step in Tutor. On Scientific Method Connection, Career Connection, Visual Connection, Evolution Connection, AP Everyday Connection. 
  - `ost-video` : Goes on any `ost-assessed-feature` that has a video.
  - `ost-exercise-choice` : Used for a group of exercises which will be used in the i-reading, but will be pre-processed by Tutor first. No examples yet in AP Bio.
  - `ost-reading-discard` : On Chapter Outline, Key Terms, Chapter Summary, Visual Connection Questions, Review Questions, Critical Thinking Questions, AP Test Prep questions, Answer Key. 
  - `ost-assignable`: On AP Science Practices Connection.   
  - `ost-learning-objective-def` : Place on the learning objective text that defines the Program Learning Objective (PLO) 
  - `ost-standards-def` : Generic standards definition class. Place on the class that defines the AP standards items. Only occurs in AP Connection. 
  - `ost-standards-apbio` : Specific AP Bio standards definition class. Place on the class that defines the AP Standard name and its definition. 
   - `ost-standards-name` : Generic class that defines the AP standard name (e.g., Big Idea 4 or Enduring Understanding 4.2.
  - `ost-standards-description` : Generic class that defines the AP standard text description. 
  - `ost-standards-discard`: Only needed if W&N adding colons or dashes between AP standard name and description. Resolve.
- no prefix: visual styling only


# Templates

`<p>` and `<a>` are used throughout instead of `<para>` and `<link>` mainly for brevity and readability.

## Key Terms

Contains `key-terms` so Tutor can hide them if necessary.

```html
  <table class="key-terms ost-reading-discard">
    <title>Key Terms</title>
    ...
  </table>
```

## Program Learning Objectives, AP Standards Defined

For biology, Program Learning Objectives do **NOT** map to the AP Learning Objectives in any way. 

```html
<section class="ap-connection">
  ... 
  <p>In this section, you will explore the following questions:</p>
  <list>
    <item class="ost-learning-objective-def ost-tag-lo-apbio-ch04-s01-lo02">How does the fluid mosaic model describe the structure and components of the plasma cell membrane?</item>
    ...
  </list>
</section>
    ... Alina to advise the CNXML for the AP table here... 
```


## Sections

```html
<section class="ost-tag-lo-apbio-ch04-s01-lo01 ost-tag-std-apbio-lo-2-10 ost-tag-std-apbio-lo-2-11">
  <title>...</title>
</section>
```

## Exercises

```html
<exercise class="os-exercise">
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/apbio-ch04-ex034" />
    </para>
  </problem>
</exercise>

```

## Things that get converted to a separate step

### Text Features

Required classes: 

One of `experiment` `career` `evolution` `visual-connection` `evolution` AND `ost-feature` and `ost-tag-std-apbio-lo-?-?`

<note class="experiment ost-feature ost-tag-std-apbio-lo-2-10">
...
</note>

### AP Science Practices Connection 

Requuired classes: 

For those WITHOUT nested questions: `ap-science-practices` AND `ost-tag-std-apbio-lo-?-?`AND  `ost-feature` 
For those WITH nested question(s):  `ap-science-practices` AND `ost-tag-std-apbio-lo-?-?` AND `ost-assessed-feature`


```html
<note class="ost-assessed-feature ap-science-practices">
  <title class="ost-tag-std-apbio-lo-2-11 ost-tag-std-apbio-lo-2-12">Applying the  
  Science Practices</title>
<note class=”ost-tag-std-apbio-lo-2-1 ost-tag-std-apbio-sciprac-1-4”>
	<label/>
    		<title>Activity</title>
    		<para>...</para>
</note>
<note>
	<label/>
<title>Lab Investigation</title>
</note>
<note>
<label/>	
<title>Questions</title>...
 	 	<exercise class="os-exercise">
	 	   <label>Questions</label>
 	 		<problem>
      				<para>
<link class="os-embed" url="..." />
</para>
</problem>
</exercise>
…
</note>
  </note>
```

### Video

For now we will NOT add os-embed to videos in Link to Learning. 


### Interactives

No interactives in AP Bio. 

### Link to Learning

TO DO: Need to add example of Link to Learning with nested question.

<note class=“link-to-learning ost-assessed-feature”>
	<label>Link to Learning</label>
	<title>...</title>
	<para> Click <a
        url="http://openstaxcollege.org/l/ice_lattice2”>here</a> to see a 3-D animation of the  
                structure of an ice lattice.
	</para>
</note>

## Misc

### Tips for Success

```html
<note class="tip tips-for-success">
  <label>Tips for Success</label>
  ...
</note>
```


## Teacher Content

Notes: 
 - Teacher content should be placed within the content that it is nearest. If it cannot be placed within that content, it should be placed just after the content.
 - Teacher content **must not** contain any solutions. Those will be placed in Exercises via the assessment import spreadsheet. The import spreadsheet can specify whether an answer should be available to students or just to teachers and that will become some sort of flag in Exercises, for when 'embargoing' is possible. 

TO DO: Go over these with Alina.

### Container

```html
Tips for Teaching
<note class="tip os-teacher">
  <label>Tips for Teaching</label>
  ...
</note>
```

```
Warm up
<note class=”os-teacher”>
  <label>Warm up</label>
  …
</note>
```

```
Launch
<note class=”os-teacher”>
  <label>Launch</label>
  …
</note>
```

```
Teach
<note class=”os-teacher”>
  <label>Teach</label>
  …
</note>
```

```
<note class=”os-teacher”>
  <label>Teacher Edition</label>
  …
</note>
```

```
Background Information
<note class=”os-teacher”>
  <label>Background Information</label>
  …
</note>
```

```
Tips for Engaging
<note class=”tip os-teacher”>
  <label>Tips for Engaging</label>
  ....
</note>
```

## Assessments

**Note:** The tutor-only assessments **must NOT** appear in the CNXML modules. 

### Practice Problems

Practice problems occur after worked examples within the flow of the section content. Tutor should use them to choose a problem for the student to work, and provide an alternate if the student gets that one wrong and wants to try another problem. 

```html
<section class="practice-problems ost-exercise-choice">
  <title>Practice Problems</title>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
</section>
```

## End of Section Review 

### Practice Concepts -> Displays as "Check your Understanding"

**NOTE:** There will be multiple practice-concepts back-to-back. And "Check your Understanding" should appear only once per group."
```html
<section class="practice-concepts ost-reading-discard">
  <title>Check Your Understanding</title>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
</section>

```

## Assessments that may be collated

### Chapter Review 

**Note:** `chapter-review` has several different variants: `concept` `problem` `critical-thinking` `performance` . Because the title Chapter Review does not make sense in the context of a module on web view, do not add Chapter Review to the <title> tag for chapter-review elements. However, Chapter Review will be added as a header to the PDF when the items are collated from multiple sections, as required by the Design Template.

```html
<section class="ost-reading-discard chapter-review concept">
  <title>Concept Items</title>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
</section>
```
### Chapter Review Performance Task

**Note:** `chapter-review performance` is discarded from Tutor's i-reading and can be assigned as a separate step (similar to Snap Labs). 

```html
<section class="ost-reading-discard ost-assignable chapter-review performance ost-tag-ngss-k12phys-*">
  <title>Performance Task</title>
  <exercise class="os-exercise">
    <problem>
      <para><link class="os-embed" url=“#ost/api/ex/k12phys-ch??-ex???" /></para>
    </problem></exercise>
</section>
```

### Test Prep

**Note:** `test-prep` has several different variants : `multiple-choice` `short-answer` `extended-response` The <title> tag must include Test Prep so that the full title appears in Web View. The PDF will overwrite this title to replace “Test Prep Extended Response” with “Extended Response” as required by the Design Template.

```html
<section class="ost-reading-discard test-prep multiple-choice">
  <title>Test Prep Multiple Choice</title>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
</section>
```
## Other potentially collated items

### Key Equations

```html
<section class="ost-reading-discard key-equations">
  <title>Key Equations</title>
  <equation>...</equation>
  <equation>...</equation>
</section>
```

### Key Terms Defined / Glossary

```html
<glossary class="ost-reading-discard">
  <definition><term>dynamics</term>
     <meaning>the study of how forces affect the motion of objects and systems</meaning>
  </definition>
</glossary>
```

### Section Summary

```html
<section class="summary ost-reading-discard">
  <title>Section Summary</title>
  <list>
    <item>Dynamics is the study of how forces affect the motion of objects such as:
      <list><item>Pushes</item><item>Pulls</item></list>
    </item>
    <item>Force is a push or pull that can be defined in terms of various <emphasis effect="italics">standards</emphasis>. It is a vector and so has both magnitude and direction.</item><item>External forces are any forces from outside of a body that act on the body. A free-body diagram is a drawing of all external forces acting on a body.</item>
  </list>
</section>
```

# Full Tag List

These are all class attributes on various CNXML elements.

## Tutor-specific

- Tags - become tags on Exercises, some used for Tutor processing
  - `ost-tag-lo-apbio-ch04-s01-lo01`
  - `ost-tag-std-apbio-4`
  - `ost-tag-std-apbio-4-a`
  - `ost-tag-std-apbio-4-a-3-a`
  - `ost-tag-std-apbio-lo-2-10`
  - `ost-tag-std-apbio-sciprac-4-2`
  - `ost-tag-blooms-1`
  - `ost-tag-dok-1`
  - `ost-tag-time-short`
  - `ost-tag-time-med`
  - `ost-tag-time-long`
- Task Steps
  - `os-exercise` with `os-embed`
  - `ost-video` with `os-embed`
  - `ost-assessed-feature` with optional `os-embed
  - `ost-feature` (means it's a step, but doesn't need any other special handling)
- Misc
  - `os-teacher`
  - `ost-reading-discard`
  - `ost-standards-apbio`
  - `ost-standards-def` (and include ost-tag-* next to this tag)
  - `ost-standards-name`
  - `ost-standards-description`
  - `ost-learning-objective-def` (for PLO’s)
  - `ost-standards-discard` (for big idea/EU, EK, SP)
- no prefix: visual styling only

## Visual-only

- `ap-connection` : AP Connection 
- `experiment` : Scientific Method Connection (existing class name from AP Bio template)
- `evolution` : Evolution Connection (existing class name from AP Bio template)
- `career` : Career Connection (existing class name from AP Bio template)
- `ap-science-practices` : AP Science Practices Connection 
- `interactive` : Link to Learning (existing class name from AP Bio template)
- `visual-connection` : Visual Connection (replacing Art Connection)
- `ap-everyday` : AP Everyday Connection 
- `key-terms`
- Exercises **Note:** Tutor doesn't use the exercise types within the module content, but these do end up as tags on the exercises in Exercises and are used to set up HWs and Reading Review problems. 
  - Within the flow of content
    NONE
  - At the End of Section
    NONE
  - End of Section Collatable Assessments
    - `visual-exercise`
    - `multiple-choice` : chapter review questions (existing class name from AP Bio template)
    - `free-response` : critical thinking questions (existing class name from AP Bio template)
    - `ap-test-prep` : AP Test Prep questions
- End of Section Collatable Features
    - `summary`
    - `glossary`(do we have a glossary?)
