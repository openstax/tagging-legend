# To Do

- Fix up the grammar, especially for things that I added, not sure what is needed.
- Decide whether exercise-block is needed anymore
- Decide how to indicate that practice-problems are treated specially by Tutor: student sees one, gets another if they miss that one. 

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
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-teks-*`: ie `ost-tag-teks-112-39-c-4c`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : On `fun-in-physics` `work-in-physics` `boundless-physics` `link-to-physics` `ost-interactive` `ost-video` `ost-snap-lab` because these each come with instructions, a feature, and a `grasp-check` assessment.
  - `ost-feature` : A non-assessed feature that should be a step in Tutor. The only one is `worked-example` for K12 physics.
  - `ost-video` : Goes on `watch-physics` and if possible any `ost-assessed-feature` that has a video.
  - `ost-interactive` : On simulations which is `virtual-physics`
  - `ost-exercise-block` : Not sure of purpose, may be able to remove 
  - `ost-reading-discard` : On `snap-lab` and end of section items, including `key-equations` `key-terms` `glossary` `summary` `ost-exercise-block` `practice-concepts`
  - `ost-assignable`: Only on `snap-lab`s. 
  - `ost-teks-def` : Place on the text of the TEKS in teacher-content that tells what that TEKS addresses
  - `ost-learning-objective-def` : Place on the learning objective text that defines the LO 
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

## Learning Objectives Defined

Note that for physics, the TEKS tags only appear on the learning objectives or in the TEKS text in teacher's edition content, and NOT on any other elements. The LOs map to one TEKS and every use of that LO implies use of that TEKS. Tutor needs to learn this mapping. The mapping should end up in Linkify eventually.

```html
<section class="learning-objectives">
  <title>Section Learning Objectives</title>
  <p>By the end of this section, you will be able to:</p>
  <list>
    <item class="ost-learning-objective-def ost-tag-lo-k12phys-ch04-s01-lo01 ost-tag-teks-112-39-c-4c">Differentiate between force, net force and dynamics</item>
    ...
  </list>
</section>
```


## Sections

```html
<section class="ost-tag-lo-k12phys-ch04-s01-lo01 ost-tag-blooms-1">
  <title>...</title>
</section>
```

## Exercises

```html
<exercise class="os-exercise">
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/k12phys-ch04-ex034">[exercise]</a>
    </para>
  </problem>
</exercise>

<exercise class="os-exercise grasp-check">
  <problem>
    <para>
      <a class="os-embed" href="#ost/api/ex/k12phys-ch12-ex099">[exercise]</a>
    </para>
  </problem>
</exercise>
```

## Things that get converted to a separate step

### Text Features

Required classes: one of `fun-in-physics` `work-in-physics` `boundless-physics` `link-to-physics` and `ost-assessed-feature`

<note class="fun-in-physics ost-assessed-feature">
...
</note>

### Snap Lab

Required classes: `snap-lab ost-assignable ost-assessed-feature ost-reading-discard`

Optional classes:

- `safety-warning`
- `students-1`, `students-2`, `students-group`

```html
<note class="ost-assignable ost-reading-discard ost-assessed-feature snap-lab students-1">
  <label>Snap Lab</label>
  <title>...</title>
  ...
</note>


<note class="ost-assignable ost-reading-discard ost-assessed-feature snap-lab students-group safety-warning ost-tag-lo-k12phys-ch04-s01-lo01 ost-tag-blooms-1 ost-tag-dok-1 ost-tag-time-short">
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
    <problem>
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
</note>
```

### Worked Example(s)

**NOTE:** Should each wrked example be a separate step if there is more than 1 worked example?

```html
<note class="ost-feature worked-example">
  <label>Worked Example</label>
  <exercise>
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
    <commentary>...</commentary>
  </exercise>
</note>


<note class="ost-feature worked-examples">
  <label>Worked Examples</label>
  <exercise>
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
    <commentary>...</commentary>
  </exercise>
</note>
```

### Video

`watch-physics` features all need to have `ost-video` added to them. The links inside them need to have `os-embed` added.

If a text feature (`fun-in-physics`, `work-in-physics`, `boundless-physics`, `link-to-physics`) has "... this <a>video</a>..." then it would be nice if the entire feature could have an `ost-video` class on it. This may not be able to be done by an external team though, so hopefully Tutor can treat them as an embed even though the embed is only on the link. 

```html

<note class="ost-assessed-feature ost-video watch-physics">
  <label>Watch Physics</label>
  <title>Calculating Average Velocity or Speed</title>
  <p>This <a class="os-embed ost-video" href="https://youtube.com/watch?askjdh">video</a> reviews vectors...</p>
  <exercise class="os-exercise grasp-check"><problem><para>
    <a class="os-embed" href="...">[exercise]</a>
  </para></problem></exercise>
</note>
```

### Interactives

**NOTE:** Not sure what to do about Flash (SWF) interactives yet. Probably need another class or use the CNXML `<embed>`.

```html
<!-- Without a grasp check -->
<note class="ost-interactive virtual-physics">
  <label>Virtual Physics</label>
  ...
  <media ... iframe width="" height="" class="os-embed" src="..." />
  ...
</note>

<!-- With a grasp check -->
<note class="ost-assessed-feature ost-interactive virtual-physics">
  <label>Virtual Physics</label>
  ...
  <iframe class="os-embed" src="..." />
  ...
  <exercise class="os-exercise grasp-check"><problem><para>
    <a class="os-embed" href="...">[exercise]</a>
  </para></problem></exercise>
</note>
```


## Misc

### Tips for Success

```html
<note class="tip tip-for-success">
  <label>Tips for Success</label>
  ...
</note>
```


## Teacher Content

Notes: 
 - Teacher content should be placed within the content that it is about, or just before the content if the element cannot have teacher content inside it.
 - Teacher content should NOT contain any solutions. Those will be placed in Exercises via the assessment import spreadsheet. The import spreadsheet can specify whether an answer should be available to students or just to teachers and that will become some sort of flag in Exercises, for when 'embargoing' is possible. 

### Container

```html
<note class="os-teacher">
  <p>Students are usually bored by this but the simulation engages them. Try to jump to the sim first</p>
    <list>
      <item class="ost-tag-teks-112-39-c-4c ost-teks-def">(4C) analyze and describe accelerated motion in two dimensions using equations, including projectile and circular examples [TEKS-112-39-C-4C]</item>
    </list>
</note>
```

### Special classes within teacher content

####Teacher Misconception Alert

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
<note class="teacher-demonstration">
  <label>Demonstration</label>
  ...
</note>

## Assessments

**Note:** The tutor-only assessments will NOT appear in the CNXML modules. 

### Practice Problems

Practice problems occur after worked examples within the flow of the section content. Tutor should use them to choose a problem for the student to work, and provide an alternate if the student gets that one wrong and wants to try another problem.

```html
<section class="practice-problems ">
  <title>Practice Problems</title>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
</section>
```

## End of Section Review 

### Practice Concepts -> Displays as "Check your Understanding"

**NOTE:** There be multiple practice-concepts back-to-back. And "Check your Understanding" should appear only once per group."
```html
<section class="practice-concepts ost-reading-discard">
  <title>Check Your Understanding</title>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
</section>

```

## Assessments that may be collated

### Chapter Review 

**Note:** `chapter-review` has several different variants: `concept` `problem` `critical-thinking` `performance`

```html
<section class="ost-exercise-block ost-reading-discard chapter-review concept">
  <title>Concepts</title>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
</section>
```
### Test Prep

**Note:** `test-prep` has several different variants : `multiple-choice` `short-answer` `extended-response`

```html
<section class="ost-exercise-block ost-reading-discard test-prep multiple-choice">
  <title>Multiple Choice</title>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
  <exercise class="os-exercise">
    <problem>
      ...
      <para><a class="os-embed" href="...">[exercise]</a></para>
    </problem>
  </exercise>
</section>
```
## Other potentially collated items

### Key Equations

```html
<section class="ost-reading-discard key-equations">
  <equation>...</equation>
  <equation>...</equation>
</section>
```

### Key Terms Defined / Glossary

```html
<glossary class="ost-reading-discard glossary">
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
  - `ost-feature` (means it's a step)
- Misc
  - `os-teacher`
  - `ost-reading-discard`
  - `ost-assignable` (always also has `ost-reading-discard`)
  - `ost-learning-objective-def`
  - `ost-teks-def`

## Visual-only

- `learning-objectives`
- `tip`
- `grasp-check`
- `snap-lab`
  - `students-1`
  - `students-2`
  - `students-group`
  - `safety-warning`
- `example-problem`
- `example-problems`
- `key-terms`
- Videos
  - `watch-physics`
- Simulations
  - `virtual-physics`  
- Features
  - `links-in-physics`
  - `fun-in-physics`
  - `work-in-physics`
  - `boundless-physics`
- Exercises
  - Within or at the End of Section
    - `practice-concepts`
    - `practice-problems`
  - End of Chapter Assessment
    - `chapter-review`
      - `concept`
      - `critical-thinking`
      - `problem`
      - `performance`
    - `test-prep`
      - `multiple-choice`
      - `short-answer`
      - `extended-response`
  - End of Chapter Features
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
