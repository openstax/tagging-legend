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
    - `os-embed`: URL to use to pull the exercise
- `ost-*`: Only OST cares about
  - `ost-tag-*`
    - `ost-tag-lo-*`: ie `ost-tag-lo-k12phys-ch12-s01-lo04` use k12phys to distinguish from college physics
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-teks-*`: ie `ost-tag-teks-112-39-c-4c`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : On `fun-in-physics` `work-in-physics` `boundless-physics` `link-to-physics` `ost-interactive` `ost-video` `ost-snap-lab` because these each come with instructions, a feature, and a `grasp-check` assessment.
  - `ost-feature` : A non-assessed feature that should be a step in Tutor (i.e. `worked-example`)
  - `ost-video`
  - `ost-interactive` : On simulations
  - `ost-reading-discard` : On `snap-lab` and end of section items like `key-equations` `ost-exercise-block`
  - `ost-assignable`: On `snap-lab`s. Also, always also has `ost-reading-discard`
- no prefix: visual styling only


# Templates

`<p>` and `<a>` are used throughout instead of `<para>` and `<link>` mainly for brevity and readability.

## Module Abstract

Contains `key-terms` so Tutor can hide them if necessary.

```html
<abstract>
  <table class="key-terms">
    <title>Key Terms</title>
    ...
  </table>
</abstract>
```


## Sections

```html
<section class="ost-tag-lo-k12phys-ch04-s01-lo01 ost-tag-blooms-1 ost-tag-teks-112-39-c-4c">
  <title>...</title>
</section>
```

## Exercises

```html
<exercise class="os-exercise">
  <problem>
    ...
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


<note class="ost-assignable ost-reading-discard ost-assessed-feature snap-lab students-group safety-warning ost-tag-lo-k12phys-ch04-s01-lo01 ost-tag-blooms-1 ost-tag-teks-112-39-c-4c ost-tag-dok-1 ost-tag-time-short">
  <label>Snap Lab</label>
  <title>Looking at Motion from two Reference Frames</title>
  <p>In this activity you will...</p>
  <p class="stem">Which frame is correct?</p>
  <list class="materials">
    <label>Materials</label>
    <item>Tennis Ball</item>
  </list>
  <list class="warnings">
    <label>Warnings</label>
    <item>Fire Risk</item>
  </list>
  <exercise class="os-exercise grasp-check">
    <problem>
      <para>What is 2+2?</para>
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

If a feature has "... this <a>video</a>..." then the entire feature should have an `ost-video` class on it

```html
<note class="ost-assessed-feature ost-video">
  <label>...</label>
  ...<a class="os-embed" href="...">video</a>...
  <exercise class="os-exercise grasp-check">...</exercise>
</note>


<note class="ost-assessed-feature ost-video watch-physics">
  <label>Watch Physics</label>
  <title>Calculating Average Velocity or Speed</title>
  <p>This <a class="os-embed" href="https://youtube.com/watch?askjdh">video</a> reviews vectors...</p>
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


### Teacher Edition

```html
<note class="os-teacher">
  <p>Students are usually bored by this but the simulation engages them. Try to jump to the sim first</p>
</note>
```

### Teacher Misconception Alert

```html
<note class="tip misconception">
  <label>Misconception Alert</label>
  ...
</note>
```

### Teacher Above/At/Below level

Needs feedback from Kim/Jason/Fred

```html
<span class="level-above">[AL]</span>
<span class="level-on">[OL]</span>
<span class="level-below">[BL]</span>
```



<note class="teacher-demonstration">
  <label>Demonstration</label>
  ...
</note>
## End of Section/Chapter

### Practice Concept/Problem

**NOTE:** There be multiple practice-concepts back-to-back. And "Check your Understanding" should appear only once per group."

```html
<section class="practice-concepts">
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


<section class="practice-problems">
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

### End of Chapter

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

### Key Equations

```html
<section class="ost-reading-discard key-equations">
  <equation>...</equation>
  <equation>...</equation>
</section>
```


# Full Tag List

These are all class attributes on various CNXML elements.

## Tutor-specific

- Topics and Tags
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
  - `ost-assessed-feature`
  - `ost-feature` (means it's a step)
- Misc
  - `os-teacher`
  - `ost-reading-discard`
  - `ost-assignable` (always also has `ost-reading-discard`)

## Visual-only

- `tip`
- `grasp-check`
- `snap-lab`
  - `students-1`
  - `students-2`
  - `students-group`
  - `safety-warning`
- `sample-problem`
- `sample-problems`
- Features
  - `watch-physics`
  - `fun-in-physics`
  - `work-in-physics`
  - `boundless-physics`
- Exercises
  - End of Section
    - `practice-concepts`
    - `practice-problems`
  - End of Chapter
    - `chapter-review`
      - `concept`
      - `critical-thinking`
      - `problem`
      - `performance`
    - `test-prep`
      - `multiple-choice`
      - `short-answer`
      - `extended-response`
    - `key-equations`
    - `section-summary`
    - `key-terms-defined`

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
    
    // "Sample Problem" or "Sample Problems"
    &.sample-problem,
    &.sample-problems, { 
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
