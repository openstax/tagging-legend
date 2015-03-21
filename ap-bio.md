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
    - `ost-tag-lo-ap-bio-*`: ie `ost-tag-lo-ap-bio-ch12-s01-lo04` use these to identify Program LO's
    - `ost-tag-ap-bio-*`: ie `ost-tag-ap-bio-4` use these to identify Big Ideas
    - `ost-tag-ap-bio-*-*`ie `ost-tag-ap-bio-4-a` use these to identify Enduring Understanding
    - `ost-tag-ap-bio-*-*-*-*`ie `ost-tag-ap-bio-4-a-3-a` use these to identify Essential Knowledge
    - `ost-tag-ap-bio-*-`ie `ost-tag-ap-bio-lo-2-10` use these to identify AP Learning Objectives
    - `ost-tag-ap-bio-sciencepractice-*-*`ie `ost-tag-science-practice-ap-bio-4-2` use these to identify Science Practices
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : On AP Science Practices Connection IF it has a nested question. 
  - `ost-feature` : This is a non-assessed feature that should be a step in Tutor. On AP Science Practices Connection IF there is no nested question, Scientific Method Connection, Career Connection, Visual Connection, Evolution Connection, AP Everyday Connection. 
  - `ost-video` : Goes on any `ost-assessed-feature` that has a video.
  - `ost-exercise-choice` : Used for a group of exercises which will be used in the i-reading, but will be pre-processed by Tutor first. Does not occur right now.
  - `ost-reading-discard` : On Chapter Outline, AP Connection, Key Terms, Chapter Summary, Visual Connection Questions, Review Questions, Critical Thinking Questions, AP Test Prep questions, Answer Key. 
  - `ost-assignable`: Not applicable to Bio. 
  - `ost-learning-objective-def` : Place on the learning objective text that defines the Program Learning Objective (PLO) 
  - `ost-standards-ap-def` : Generic standards definition class. Place on the class that defines the AP standards items. Only occurs in AP Connection. 
  - `ost-standards-ap` : Specific AP standards definition class. Place on the class that defines the AP Standard name and its definition. 
   - `ost-standards-ap-name` : Generic class that defines the AP standard name (e.g., Big Idea 4 or Enduring Understanding 4.2.
  - `ost-standards-ap-description` : Generic class that defines the AP standard text description. 
  - `ost-standards-ap-discard`: Only needed if W&N adding colons or dashes between AP standard name and description. Resolve.
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
    <item class="ost-learning-objective-def ost-tag-lo-ap-bio-ch04-s01-lo02">How does the fluid mosaic model describe the structure and components of the plasma cell membrane?</item>
    ...
  </list>
</section>
    ... Alina to advise the CNXML for the AP table here... 
```


## Sections

```html
<section class="ost-tag-lo-ap-bio-ch04-s01-lo01 ost-tag-ap-bio-lo-2-10 ost-tag-ap-bio-lo-2-11">
  <title>...</title>
</section>
```

## Exercises

```html
<exercise class="os-exercise">
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/ap-bio-ch04-ex034" />
    </para>
  </problem>
</exercise>

```

## Things that get converted to a separate step

### Text Features

Required classes: 

One of Scientific Method Connection, Career Connection, Visual Connection, Evolution Connection AND `ost-feature` and `ost-tag-ap-bio-lo-?-?`For AP Science Practices Connection, you need its class AND `ost-tag-ap-bio-lo-?-?`AND EITHER `ost-feature` or `ost-assessed-feature` depending on whether it has a question.

<note class="fun-in-physics ost-assessed-feature ost-tag-lo-k12phys-ch12-s01-lo04">
...
</note>

### Snap Lab

Required classes: `snap-lab ost-assignable ost-assessed-feature ost-reading-discard``ost-tag-lo-k12phys-ch??-s??-lo??`

Optional classes:

- `safety-warning`
- `students-1`, `students-2`, `students-group`

```html
<note class="ost-assignable ost-reading-discard ost-assessed-feature snap-lab students-? ost-tag-lo-k12phys-ch??-s??-lo??">
  <label>Snap Lab</label>
  <title>...</title>
  ...
</note>


<note class="ost-assignable ost-reading-discard ost-assessed-feature snap-lab students-group safety-warning ost-tag-lo-k12phys-ch04-s01-lo01">
  <label>Snap Lab</label>
  <title>Looking at Motion from two Reference Frames</title>
  <list class="materials">
    <label>Materials</label>
    <item>Tennis Ball</item>
  </list>
  <list class="warnings">
    <label>Warnings</label>
    <item>Fire Risk</item>
  </list>
    <p>In this activity you will...</p>
  <p>Which frame is correct?</p>
  <exercise class="os-exercise grasp-check">
    <label>Grasp Check</label>
    <problem>
      <para><a class="os-embed" href="..." /></para>
    </problem>
  </exercise>
</note>
```

### Worked Example(s)

When there is more than one worked example, multiple examples will live in the same container and will not be converted to a separate step. We add a class that includes the ExerciseID for the Worked Example's multiple-choice "clone" in Exercises.

```html
<note class="ost-feature worked-example ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Worked Example</label>
  <exercise class="ost-k12phys-ch04-ex034">
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
<commentary><title>Discussion</title><para>...</para></commentary>
  </exercise>
</note>


<note class="ost-feature worked-examples ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Worked Examples</label>
  <exercise class="ost-k12phys-ch04-ex035">
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
    <commentary><title>Discussion</title><para>...</para></commentary>
  </exercise>
  <exercise class="ost-k12phys-ch04-ex036">
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
    <commentary><title>Discussion</title><para>...</para></commentary>
  </exercise>
</note>
```

### Video

`watch-physics` features all need to have `ost-video` added to them. The links inside them need to have `os-embed` added.

If a text feature (`fun-in-physics`, `work-in-physics`, `boundless-physics`, `links-to-physics`) has "... this <a>video</a>..." then it would be nice if the entire feature could have an `ost-video` class on it. This may not be able to be done by an external team though, so hopefully Tutor can treat them as an embed even though the embed is only on the link. 

```html

<note class="ost-assessed-feature ost-video watch-physics ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Watch Physics</label>
  <title>Calculating Average Velocity or Speed</title>
  <p>This <a class="os-embed" href="https://youtube.com/watch?askjdh">video</a> reviews vectors...</p>
  <exercise class=“os-exercise grasp-check”>
  <label>Grasp Check</label>
    <a class="os-embed" href="..." />
  </para></problem></exercise>
</note>
```

### Interactives

**NOTE:** Unsure what to do about Flash (SWF) interactives yet. Probably need another class or use the CNXML `<embed>`.

```html
<!-- Without a grasp check -->
<note class="ost-interactive virtual-physics ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Virtual Physics</label>
  ...
  <media alt=“…” class=“os-embed><iframe width=“960” height=“785” src=“…”/></media>
  ...
</note>

<!-- With a grasp check -->
<note class="ost-assessed-feature ost-interactive virtual-physics ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Virtual Physics</label>
  ...
  <media alt=“…” class=“os-embed><iframe width=“960” height=“785” src=“…”/></media>
  ...
  <exercise class=“os-exercise grasp-check”>
  <label>Grasp Check</label>
  <problem><para>
    <a class="os-embed" href="..." />
  </para></problem></exercise>
</note>
```


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

### Container

```html
<note class="os-teacher">
  <label>Teacher Edition</label>
    <p>The Learning Objectives in this section will help your students master the following TEKS:</p>
      <list>
        <item>(4) Science concepts. The student knows and applies the laws governing motion in a variety of situations. The     
       student is expected to:
          <list>
            <item class="ost-standards-def ost-standards-teks ost-tag-teks-112-39-c-4c">
              <span class="ost-standards-name">(4C)</span>
              <span class="ost-standards-discard">:</span>
              <span class="ost-standards-description">analyze and 
                describe accelerated motion in two dimensions using equations, including projectile and circular
                examples</span>
            </item>
        </list>
      </item>
    </list>
</note>
```

### Special classes within teacher content

#### Teacher Content with NGSS tag

```html

<note class="os-teacher">
  <label>Teacher Edition</label>
  <list>
    <item class="ost-standards-def ost-standards-ngss ost-tag-ngss-k12phys-hs-ps2-1">
      <span class="ost-standards-name">NGSS HS-PS2-1</span>
      <span class="ost-standards-discard">:</span>
      <span class="ost-standards-description">Students who demonstrate understanding
        can: Analyze data to support the claim that Newton’s second law of motion describes the mathematical
        relationship among the net force on a macroscopic object, its mass, and its acceleration.</span>
    </item>
  </list>
</note>
```

#### Teacher Misconception Alert

```html
<note class="tip misconception">
  <label>Misconception Alert</label>
  ...
</note>
```

#### Teacher Above/At/Below level

```html
<span class="level-above">[AL]</span>
<span class="level-on">[OL]</span>
<span class="level-below">[BL]</span>
```

#### Teacher Demonstration

```html
<note class="teacher-demonstration">
  <label>Teacher Demonstration</label>
  ...
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
  - `ost-tag-lo-ap-bio-ch04-s01-lo01`
  - `ost-tag-ap-bio-4`
  - `ost-tag-ap-bio-4-a`
  - `ost-tag-ap-bio-4-a-3-a`
  - `ost-tag-ap-bio-lo-2-10`
  - `ost-tag-ap-bio-sciencepractice-4-2`
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
  - `ost-standards-ap`
  - `ost-standards-ap-def` (and include ost-tag-* next to this tag)
  - `ost-standards-ap-name`
  - `ost-standards-ap-description`
  - `ost-learning-objective-def` (for PLO’s)
  - `ost-standards-ap-discard` (for big idea/EU, EK, SP)
- no prefix: visual styling only

## Visual-only

- `ap-connection` : AP Connection 
- `experiment` : Scientific Method Connection (old)
- `evolution` : Evolution Connection (old)
- `career` : Career Connection (old)
- `ap-science-practices` : AP Science Practices Connection 
- `interactive` : Link to Learning (old)
- `visual-connection` : Visual Connection (replacing Art Connection)
- `ap-everyday-connection` : AP Everyday Connection 
- `key-terms`
- Exercises **Note:** Tutor doesn't use the exercise types within the module content, but these do end up as tags on the exercises in Exercises and are used to set up HWs and Reading Review problems. 
  - Within the flow of content
    NONE
  - At the End of Section
    NONE
  - End of Section Collatable Assessments
    - `visual-connection`
    - `multiple-choice` : chapter review questions (old TL tag)
    - `free-response` : critical thinking questions (old TL tag)
    - `ap-test-prep` : AP Test Prep questions
- End of Section Collatable Features
    - `summary`
    - `glossary`(do we have a glossary?)
