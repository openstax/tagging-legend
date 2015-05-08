# To Do

- Fix up the grammar, especially for things that were added since Phil's commit. Except for name changes, the full grammar was not updated.
- Phil to update CNXML for sims and videos.

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
  - `os-embed`: URL to use to pull exercises, videos, and simulations, that should be embedded in the content.
- `ost-*`: Only OST cares about
  - `ost-tag-*`
    - `ost-tag-lo-*`: ie `ost-tag-lo-k12phys-ch12-s01-lo04` use k12phys to distinguish from college physics
    - `ost-tag-ngss-*`: ie `ost-tag-ngss-hs-ps2-1`
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-teks-*`: ie `ost-tag-teks-112-39-c-4c`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : On `fun-in-physics` `work-in-physics` `boundless-physics` `links-to-physics` `virtual-physics` `watch-physics` `snap-lab` because these each come with instructions, a feature, and a `grasp-check` assessment.
  - `ost-feature` : A non-assessed feature that should be a step in Tutor. The only one is `worked-example` for K12 physics.
  - `ost-video` : Goes on `watch-physics`
  - `ost-interactive` : On simulations which is `virtual-physics`
  - `ost-exercise-choice` : Used for a group of exercises which will be used in the i-reading, but will be pre-processed by Tutor first. Only occurs on `os-practice-problems` right now. 
  - `ost-reading-discard` : On `snap-lab` and end of section and chapter items, including `key-equations` `key-terms` `summary`  `os-practice-concepts` `concept` `problem` `critical-thinking` `performance` `multiple-choice` `short-answer` `extended-response`
  - `ost-assignable`: Only on `snap-lab`s and `chapter-review performance`
  - `ost-learning-objective-def` : Place on the learning objective text that defines the LO 
  - `ost-standards-def` : Generic standards definition class. Place on the Next Generation Science Standards (NGSS) and TEKS class that define the TEKS or NGSS name and its definition. Only occurs on a) TS content that defines NGSS (Performance Task) and b) TS content that defines TEKS standards.
  - `ost-standards-teks` : Specific TEKS definition class. Place on the class that defines the TEKS name and its definition. 
  - `ost-standards-ngss` : Specific NGSS definition class. Place on the class that defines the NGSS name and its definition. 
  - `ost-standards-name` : Generic class that defines the TEKS or NGSS name (e.g., 4C or HS-PS2-*). 
  - `ost-standards-description` : Generic class that defines the TEKS or NGSS text description. 
  - `ost-standards-discard`: Generic class that lets UX style (i.e., remove) the : listed in the TEKS and NGSS standards
- `ost-chapter-review` : Place on `concept` `problem` `critical-thinking` `performance` so Tutor knows to use these for homework.
- `ost-test-prep`: Place on `multiple-choice` `short-answer` `extended-response` so Tutor knows to use these for practice widget. 
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

## Section Opener, including Learning Objectives Defined, the first Teacher Edition, and Section Key Terms

Note that for physics, the TEKS tags only appear on the learning objectives or in the TEKS text in teacher's edition content, and **NOT** on any other elements. The LOs map to one TEKS and every use of that LO implies use of that TEKS. Tutor needs to learn this mapping. The mapping should end up in Linkify eventually.

```html
<section class="section-opener">
<note class="learning-objectives"><label/>
  <title>Section Learning Objectives</title>
  <para>By the end of this section, you will be able to:</para>  
    <list>
    <item class="ost-learning-objective-def ost-tag-lo-k12phys-ch??-s??-lo?? ost-tag-teks-112-39-?-??">     
      ...</item>
    <item>...</item>
    </list>
</note>

<note class="os-teacher"><label>Teacher Edition</label>
<para>...:</para> 
	<list>
		<item>(4) Science concepts. ...: 
  			<list>
				<item class="ost-standards-def ost-standards-teks ost-tag-teks-112-39-c-4c">
				<span class="ost-standards-name">(??)</span>
				<span class="ost-standards-discard">:</span> 
				<span class="ost-standards-description">... </span>
				</item>
	        </list>
      	</item>
	</list>

<para><span class="ost-level-below">[BL]</span> 
<span class="ost-level-on">[OL]</span>
<span class="ost-level-above">[AL]</span> ...</para>

</note>

<table summary="W&N to provide" class="key-terms ost-reading-discard unnumbered"><label/><title>Section Key Terms</title>
<tgroup cols="3"><tbody>
  <row>
    <entry>dynamics</entry>
    <entry>external force</entry>
    <entry>force</entry>
  </row>
  <row>
    <entry>free body diagram</entry>
    <entry>net external force</entry>
    <entry>net force</entry>
  </row>
</tbody>


</tgroup>
</table>
</section>
```

## Sections

```html
<section class="ost-tag-lo-k12phys-ch04-s01-lo01">
  <title>...</title>
</section>
```

## Exercises

```html
<exercise class="os-exercise">
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/k12phys-ch04-ex034" />
    </para>
  </problem>
</exercise>

<exercise class=“os-exercise grasp-check”>
  <label>Grasp Check</label>
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/k12phys-ch12-ex099" />
    </para>
  </problem>
</exercise>
```

## Things that get converted to a separate step

### Text Features

Required classes: one of `fun-in-physics` `work-in-physics` `boundless-physics` `links-to-physics` and `ost-assessed-feature` and `ost-tag-lo-k12phys-ch??-s??-lo??`

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

Previously, we said that if a text feature (`fun-in-physics`, `work-in-physics`, `boundless-physics`, `links-to-physics`) has "... this <a>video</a>..." then add an `ost-video` class on it and `os-embed` on the link. However, per W&N confirmation, links to videos in these text features will be links (and not embedded), so only Watch Physics will have this treatment.

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
<figure><label/>
<media alt="...">
    <image mime-type="image/jpeg" src="..."/>
  </media>
  <caption>
<link url="..." class="ost-iframe-embeddable">Click here for the... simulation</link>
  </caption>
</figure>
  ...
</note>

<!-- With a grasp check -->
<note class="ost-assessed-feature ost-interactive virtual-physics ost-tag-lo-k12phys-ch12-s01-lo04">
  <label>Virtual Physics</label>
  ...
<figure><label/>
<media alt="...">
    <image mime-type="image/jpeg" src="..."/>
  </media>
  <caption>
<link url="..." class="ost-iframe-embeddable">Click here for the... simulation</link>
  </caption>
</figure>
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
<note class="tips-for-success">
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
    <item class="ost-standards-def ost-standards-ngss ost-tag-ngss-hs-ps2-1">
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
<note class="ost-misconception">
  <label>Misconception Alert</label>
  ...
</note>
```

#### Teacher Above/At/Below level

```html
<span class="ost-level-above">[AL]</span>
<span class="ost-level-on">[OL]</span>
<span class="ost-level-below">[BL]</span>
```

#### Teacher Demonstration

```html
<note class="ost-teacher-demonstration">
  <label>Teacher Demonstration</label>
  ...
</note>
```

## Assessments

**Note:** The tutor-only assessments **must NOT** appear in the CNXML modules. 

### Practice Problems

Practice problems occur after worked examples within the flow of the section content. Tutor should use them to choose a problem for the student to work, and provide an alternate if the student gets that one wrong and wants to try another problem. 

```html
<section class="os-practice-problems ost-exercise-choice">
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

**NOTE:** There will be multiple os-practice-concepts back-to-back. And "Check your Understanding" should appear only once per group."
```html
<section class="os-practice-concepts ost-reading-discard">
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

**Note:** `ost-chapter-review` goes on all of these question types: `concept` `problem` `critical-thinking` `performance` . 

Because the title Chapter Review does not make sense in the context of a module on web view, do not add Chapter Review to the `<title>` tag for chapter-review elements. However, Chapter Review will be added as a header to the PDF when the items are collated from multiple sections, as required by the Design Template. 

```html
<section class="ost-reading-discard ost-chapter-review concept">
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

**Note:** `ost-chapter-review performance` is discarded from Tutor's i-reading and can be assigned as a separate step (similar to Snap Labs). 

```html
<section class="ost-reading-discard ost-assignable ost-chapter-review performance ost-tag-ngss-*">
  <title>Performance Task</title>
  <exercise class="os-exercise">
    <problem>
      <para><link class="os-embed" url=“#ost/api/ex/k12phys-ch??-ex???" /></para>
    </problem></exercise>
</section>
```

### Test Prep

**Note:** `ost-test-prep` goes on all of these question types : `multiple-choice` `short-answer` `extended-response` The `<title>` tag must include Test Prep so that the full title appears in Web View. The PDF will overwrite this title to replace “Test Prep Extended Response” with “Extended Response” as required by the Design Template.

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
<glossary>
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
  - `ost-tag-lo-k12phys-ch04-s01-lo01`
  - `ost-tag-blooms-1`
  - `ost-tag-teks-112-39-c-4c`
  - `ost-tag-dok-1`
  - `ost-tag-time-short`
  - `ost-tag-time-med`
  - `ost-tag-time-long`
- Task Steps
  - `os-exercise` with `os-embed`
  - `ost-video` with `os-embed`
  - `ost-interactive` with `os-embed`
  - `ost-assessed-feature` with optional `os-embed`
  - `ost-exercise-choice` for os-practice-problems so we can give one to the student and then optionally follow up.
  - `ost-feature` (means it's a step, but doesn't need any other special handling)
- End-of-chapter assessments
  - `ost-chapter-review` tells Tutor questions are chapter review  
  - `ost-test-prep` tells Tutor a questions are test-prep
- Misc
  - `os-teacher`
    - `ost-misconception`
    - `ost-level-above`
    - `ost-level-on`
    - `ost-level-below`
    - `ost-teacher-demonstration`
  - `ost-reading-discard`
  - `ost-assignable` (always also has `ost-reading-discard`)
  - `ost-learning-objective-def`
  - `ost-standards-def` 
  - `ost-standards-teks`
  - `ost-standards-ngss`  
  - `ost-standards-name`
  - `ost-standards-description`
  - `ost-standards-discard` 
- no prefix: visual styling only

## Visual-only

- `learning-objectives`
- `tip`
- `grasp-check`
- `snap-lab`
  - `students-1`
  - `students-2`
  - `students-group`
  - `safety-warning`
- `worked-example`
- `worked-examples`
- `key-terms`
- Videos
  - `watch-physics`
- Simulations
  - `virtual-physics`  
- Features
  - `links-to-physics`
  - `fun-in-physics`
  - `work-in-physics`
  - `boundless-physics`
- Exercises **Note:** Tutor doesn't use the exercise types within the module content, but these do end up as tags on the exercises in Exercises and are used to set up HWs and Reading Review problems. 
  - Within the flow of content
    - `os-practice-problems`
  - At the End of Section
    - `os-practice-concepts`
  - End of Section Collatable Assessments
      - `concept`
      - `critical-thinking`
      - `problem`
      - `performance`
      - `multiple-choice`
      - `short-answer`
      - `extended-response`
- End of Section Collatable Features
    - `key-equations`
    - `summary`
    - `glossary`

# Full Grammar

```less

.x-topics() {
  // LO,text,bloom Tags
  &.ost-tag-lo-k12phys-ch04-s01-lo01,
  &.ost-tag-blooms-1,
  &.ost-tag-teks-112-39-c-4c,
  &.ost-tag-dok-1,
  &.ost-tag-time-short,
  &.ost-tag-time-med,
  &.ost-tag-time-long { }
}

.x-exercise() {
  p.os-exercise.ost-only-execise {         // because <a> tags need to be in a block
    a.os-embed { }
  }
}

.x-grasp-check() {
  p.os-exercise.ost-only-execise.grasp-check {
    a.os-embed { }
  }
}


// Things that get converted to a separate step
{
  note.ost-feature {
    &.snap-lab.ost-assignable {
      // Book-only
      &.students-1,
      &.students-2,
      &.students-group { }
      &.safety-warning { }
      .x-topics();
      .x-grasp-check();
    }
    
    // "Example Problem" or "Example Problems"
    &.example-problem,
    &.example-problems, { 
      exercise {
        problem { 
          /*
            ## Calculating Distance and Displacement
            A Cyclist rides... (a) what distance does she ride?
            ### Strategy
            aaskjhdaksjhdsakjhd
          */
        }
        solution { }
        commentary {
          /*
            # Discussion
            The displacement is negative because ...
          */
        }
      }
    }
  }
  
  note.ost-video {
    &.watch-physics, // "Watch Physics"
    &.fun-in-physics, // "Fun in Physics"
    &.work-in-physics, // "Work in Physics"
    &.boundless-physics, // "Work in Physics"
     { }

    a.os-embed { }
    .x-grasp-check();
  }

  // "Virtual Physics"
  note.ost-interactive {
    // &.virtual-physics { }
    iframe.os-embed { }
    .x-grasp-check();
  } 
  
}

// "Tips for Success"
note.tip { }

// Ignore an element when building an iReading but exercises in it are still added as steps
.ost-only-execise { }
// Ignore when just browsing the book as a student
.os-teacher { } 



section.ost-only-execise {
  // End-of-module exercises
  &.practice-concepts,
  &.practice 
    { }

  // End of chapter exercises
  &.chapter-review {
    // concept questions might all have the same ost-tag-dok-* tag on them
    // and that's all that tutor cares about.
    &.concept,
    &.critical-thinking,
    // &.problem,
    &.performance { }
  }
  &.test-prep {
    &.multiple-choice,
    &.short-answer,
    &.extended-response { }
  }

  .x-exercise();
}
```
