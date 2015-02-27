# Overview

- [CNXML Templates](#templates)
- [Full Tag List](#full-tag-list)
  - [Tutor-specific](#tutor-specific)
  - [CNX-specific](#cnx-specific)
- [Full Grammar](#full-grammar)

# Templates

`<p>` and `<a>` are used throughout instead of `<para>` and `<link>` mainly for brevity and readability.

## Sections

```html
<section class="ost-topic-phys-ch04-s01-lo01 ost-tag-bloom-1 ost-tag-teks-4b">
  <title>...</title>
</section>
```

## Exercises

```html
<p class="os-exercise ost-only-exercise">
  <a class="os-link" href="...">[exercise]</a>
</p>

<p class="os-exercise ost-only-exercise grasp-check">
  <a class="os-link" href="...">[exercise]</a>
</p>
```

## Things that get converted to a separate step

### Snap Lab

```html
<note class="ost-assignable snap-lab students-1">
  <label>Snap Lab</label>
  <title>...</title>
  ...
</note>

<note class="ost-assignable snap-lab students-group safety-warning ost-topic-phys-ch04-s01-lo01 ost-tag-bloom-1 ost-tag-teks-4b ost-tag-dok-1 ost-tag-time-short">
  <label>Snap Lab</label>
  <title>Looking at Motion from two Reference Frames</title>
  <p>In this activity you will…</p>
  <p class="stem">Which frame is correct?</p>
  <list class="materials">
    <label>Materials</label>
    <item>Tennis Ball</item>
  </section>
  <list class="warnings">
    <label>Warnings</label>
    <item>Fire Risk</item>
  </list>
  <p class="os-exercise ost-only-exercise grasp-check">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</note>
```

### Sample Problem(s)

```html
<note class="ost-reading sample-problem">
  <label>Sample Problem</label>
  <exercise>
    <title>...</title>
    <problem>...</problem>
    <solution>...</solution>
    <commentary>...</commentary>
  </exercise>
</note>
```

### Video

```html
<note class="ost-video">
  <label>...</label>
  ...
  <a class="os-link">[Video Title]</a>
  ...
</note>


<note class="ost-video watch-physics">
  <label>Watch Physics</label>
  <title>Calculating Average Velocity or Speed</title>
  <p>This <a class="os-link" href="https://youtube.com/watch?askjdh">video</a> reviews vectors…</p>
  <p class="os-exercise ost-only-exercise grasp-check">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</note>
```

### Interactives

```html
<note class="ost-interactive interactive">
  <label>Virtual Physics</label>
  ...
  <a class="os-link" href="..." />
  ...
</note>
```


## Misc

### Tips for Success

```html
<note class="tip">
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



## End of Section/Chapter exercises

### End of Section

```html
<section class="ost-only-exercise">
  <title>...</title>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</section>


<section class="ost-only-exercise formative-assessments">
  <title>Formative Assessments</title>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</section>
```

### End of Chapter

```html
<section class="ost-only-exercise chapter-review concept">
  <title>Concepts</title>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</section>


<section class="ost-only-exercise test-prep multiple-choice">
  <title>Multiple Choice</title>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
  <p class="os-exercise">
    <a class="os-link" href="...">[exercise]</a>
  </p>
</section>
```


# Full Tag List

These are all class attributes on various CNXML elements.

## Tutor-specific

- Topics and Tags
  - `ost-topic-phys-ch04-s01-lo01`
  - `ost-tag-bloom-1`
  - `ost-tag-teks-4b`
  - `ost-tag-dok-1`
  - `ost-tag-time-short`
  - `ost-tag-time-med`
  - `ost-tag-time-long`
- Task Steps
  - `os-exercise`
  - `ost-reading`
  - `ost-video`
  - `ost-interactive`
  - `os-link`
- Misc
  - `ost-only-exercise`
  - `os-teacher`
  - `ost-assignable`

## CNX-specific

- `tip`
- `grasp-check`
- `snap-lab`
  - `students-1`
  - `students-2`
  - `students-group`
  - `safety-warning`
- `sample-problem`
- `sample-problems`
- Videos
  - `watch-physics`
  - `fun-in-physics`
  - `work-in-physics`
  - `boundless-physics`
- Exercises
  - End of Section
    - `formative-assessments`
    - `practice`
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

# Full Grammar

```less

.x-topics() {
  // LO,text,bloom Tags
  &.ost-topic-phys-ch04-s01-lo01,
  &.ost-tag-bloom-1,
  &.ost-tag-teks-4b,
  &.ost-tag-dok-1,
  &.ost-tag-time-short,
  &.ost-tag-time-med,
  &.ost-tag-time-long { }
}

.x-exercise() {
  p.os-exercise.ost-only-execise {         // because <a> tags need to be in a block
    a.os-link { }
  }
}

.x-grasp-check() {
  p.os-exercise.ost-only-execise.grasp-check {
    a.os-link { }
  }
}


// Things that get converted to a separate step
{
  note.ost-reading {
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

    a.os-link { }
    .x-grasp-check();
  }

  // "Virtual Physics"
  note.ost-interactive {
    // &.interactive { }
    iframe.os-link { }
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
  &.formative-assessments,
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
