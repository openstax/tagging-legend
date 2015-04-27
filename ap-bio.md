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
    - `ost-tag-std-apbio-*-*-*-*`ie `ost-tag-std-apbio-4-a-3` use these to identify Essential Knowledge. AP Bio framework can further divide these into subtopics (e.g., 4-a-3-a) but Maria says their tags will only ever refer to the "general" stem (4-a-3).
    - `ost-tag-std-apbio-lo-*-`ie `ost-tag-std-apbio-lo-2-10` use these to identify AP Learning Objectives
    - `ost-tag-std-apbio-sciprac-*-*`ie `ost-tag-std-apbio-sciprac-4-2` use these to identify Science Practices
    - `ost-tag-blooms-*`: ie `ost-tag-blooms-1`
    - `ost-tag-dok-*`: ie `ost-tag-dok-1`
    - `ost-tag-time-*` can be one of `short`, `med`, or `long`
  - `ost-assessed-feature` : On `interactive` `visual-connection`, `ap-everyday` 
  - `ost-get-exercise` : This is on the section class. It tells Tutor that it should pull in questions (probably Concept Coach questions) after the end of the section.  
  - `ost-feature` : This is a non-assessed feature that should be a step in Tutor. On `experiment`, `career`, `evolution`. 
  - `ost-video` : Goes on any `ost-assessed-feature` that has a video.
  - `ost-exercise-choice` : Used for a group of exercises which will be used in the i-reading, but will be pre-processed by Tutor first. No examples yet in AP Bio.
  - `ost-reading-discard` : On Chapter Outline, `ap-connection`, `key-terms`, `ap-science-practices`, Chapter Summary, `visual-exercise`, `multiple-choice`, `free-response`, `ap-test-prep`, Answer Key. 
  - `ost-assignable`: On the three individual pieces -- Laboratory, Activity, and Scientific Thinking -- nested in `ap-science-practices`.  It is not on AP Science Practices itself. 
  - `ost-learning-objective-def` : Place on the learning objective text that defines the Program Learning Objective (PLO) 
  - `ost-standards-def` : Generic standards definition class. Place on the class that defines the AP standards items. Only occurs in `ap-connection`. 
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

## Program (i.e., module-level book learning objectives) Learning Objectives Defined 

Note: For biology, Program Learning Objectives do **NOT** map to the AP Learning Objectives in any way. 

```html
<section class="learning-objectives">
  <title>Learning Objectives</title>
  <para>In this section, you will explore the following questions:</para>
  <list>
    <item class="ost-learning-objective-def ost-tag-lo-apbio-ch05-s01-lo01">How does the fluid mosaic model describe the structure and components of the plasma cell membrane?</item>
    <item class="ost-learning-objective-def ost-tag-lo-apbio-ch05-s01-lo02">How do the molecular components of the membrane provide fluidity? </item>
  </list>
</section>
```

## Connection for AP® Courses

This section will retain only the opening paragraph(s) of content. We will discard from i-reading the introduction to the AP content, the descriptions of Big Idea and Enduring Understanding, and the AP LO/EK/SP tables. 

```html
<section class="ap-connection">
<title>Connection for AP® Courses</title>

<para>Organisms exchange matter … </para>

<para class="ost-reading-discard">Information presented and the examples highlighted ... </para>

<para class="ost-reading-discard ost-standards-def ost-standards-apbio ost-tag-std-apbio-?"><span class="ost-standards-name"><emphasis>Big Idea ?</emphasis></span><span class="ost-standards-description">Biological systems ...</span></para>

<para class="ost-reading-discard ost-standards-def ost-standards-apbio ost-tag-std-apbio-?-?”><span class="ost-standards-name”><emphasis>Enduring Understanding ?.?</emphasis></span><span class="ost-standards-description”>The student is able to ... </span></para>

  <table summary="Words and Numbers to provide" class="unnumbered no-title column-header ost-reading-discard"><label/>
<tbody>
<row class=“ost-standards-def ost-standards-apbio ost-tag-std-apbio-?-?-?-?”>
    <entry class=“ost-standards-name”><emphasis>Essential Knowledge</emphasis></entry>
    <entry><span class=“ost-standards-name”><emphasis>?.?.?.?</emphasis></span><span class="ost-standards-description”>The student is able to ... </span>
</entry>
  </row>

  <row class=“ost-standards-def ost-standards-apbio ost-tag-std-apbio-sciprac-?-?”>
    <entry class=“ost-standards-name”><emphasis>Science Practice</emphasis></entry>
    <entry><span class=“ost-standards-name”><emphasis>?.?</emphasis></span><entry><span class="ost-standards-description”>The student can ... </span>
</entry>
  </row>

[… if table includes more than 1 Science Practice, each Science Practice must be added to its OWN row ...] 

<row class=“ost-standards-def ost-standards-apbio ost-tag-std-apbio-lo-2-11”>
    <entry class=“ost-standards-name”><emphasis>Learning Objective</emphasis></entry>
    <entry><span class=“ost-standards-name”><emphasis>2.11</emphasis></span><span class="ost-standards-description”>The student is able to construct models that connect the movement of molecules across membrane with membrane structure and function.</span>
</entry>
  </row>

</tbody>
</tgroup>
</table>

```


## Sections

These must have `ost-get-exercise` `ost-tag-lo-apbio-ch??-s??-lo??` and `ost-tag-std-apbio-lo-?-??`

```html
<section class="ost-get-exercise ost-tag-lo-apbio-ch04-s01-lo01 ost-tag-std-apbio-lo-2-10 ost-tag-std-apbio-lo-2-11">
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

### Text Features with assessments

Required classes: one of `experiment` `ap-everyday` `interactive` `evolution`  AND `ost-assessed-feature` AND `ost-tag-std-apbio-lo-?-?` In some cases, features may also have `ost-tag-lo-apbio-ch??-s??-lo??`.

#### Visual Connection

Note: XML team will be removing the text of the visual connection questions and adding in os-embed so that we can link to the questions in Exercises. 

```html
<note class="visual-connection ost-assessed-feature ost-tag-std-apbio-lo-2-10">
<label/><title>Visual Connection</title>
<para><figure><media alt=“…”>
<image mime-type="image/png" src=“…” />
</media>
<caption>…</caption></figure></para>
<exercise class="os-exercise">
<problem>
<para>
<link class="os-embed" url=“#ost/api/ex/apbio-ch??-ex???" />
</para>
</problem>
</exercise>
…(room for multiple exercises)
</note>
```

#### Everyday Connection for AP® Courses
```html
<note class="ap-everyday ost-assessed-feature ost-tag-std-apbio-lo-2-10"><label>Everyday Connection for AP® Courses Connection</label><title>…</title><para>…</para>
<exercise class="os-exercise”>
<problem>
<para>
<link class="os-embed" url=“#ost/api/ex/apbio-ch??-ex???" />
</para>
</problem>
</exercise>
</note>

```

#### Link to Learning

CNXML team to add nested exercises within this element. We are NOT having them change the link to os-embed until we have more information about permissions. 

```html
<note class="interactive ost-assessed-feature ost-tag-std-apbio-lo-?-?`"><label/><title>Link to Learning</title>
<media alt="QR Code representing a URL">
<image mime-type="image/png" src=“…”/>
</media>
<para>…</link>.</para>
<exercise class="os-exercise">
<problem>
<para>
<link class="os-embed" url=“#ost/api/ex/apbio-ch??-ex???" />
</para>
</problem>
</exercise>
</note>
```

#### Evolution Connection
```html
<note class="evolution ost-assessed-feature ost-tag-std-apbio-lo-2-10">
<label/>
<title>Evolution Connection</title>
<para>
<title>Carbon Dating</title>
…</para>
<figure><media alt=“…”>
    <image mime-type="image/jpg" src=“…” />
</media>
<caption>…</caption>
</figure>
<exercise class="os-exercise">
<problem>
<para>
<link class="os-embed" url=“#ost/api/ex/apbio-ch??-ex???" />
</para>
</problem>
</exercise>
</note>

```

### Text Features without assessments

Required classes: 

One of `career` and `experiment` AND `ost-feature` AND `ost-tag-std-apbio-lo-?-?`

In some cases, features may also have `ost-tag-lo-apbio-ch??-s??-lo??`.

#### Career Connection
```html
<note class="career ost-feature ost-tag-std-apbio-lo-2-10">
...
</note>
```

#### Scientific Method Connection
```html
<note class="experiment ost-feature ost-tag-std-apbio-lo-2-10">
...
</note>
```

## Text Features that are assignable outside of interactive reading 

### Science Practice Connection for AP® Courses 

NOTE: 
The container requires `ap-science-practices` and `ost-reading-discard`. The overall `ap-science-practices` container does not have `ost-assignable` but its individual pieces (Activity, Lab Investigation, and Think About It) must. 

```html
<note class=“ap-science-practices ost-reading-discard”>
<label>Science Practice Connection for AP® Courses</label>

<note class=“ost-assignable ost-sciprac-activity ost-tag-std-apbio-lo-?-??”>
<label/>
<title>Activity</title>
<para>…</para>
</note>

<note class=“ost-assignable ost-sciprac-lab ost-tag-std-apbio-lo-?-??”>
<label/>
<title>Lab Investigation</title>
<para>[content content content]</para>
</note>

<note class=“ost-assignable ost-sciprac-scithink”>
<label/>
<title>Scientific Thinking</title>
<exercise class=“ost-tag-std-apbio-lo-?-??”><problem><para>...</para></problem></exercise>
<exercise class=“ost-tag-std-apbio-lo-?-??”><problem><para>...</para></problem>
</exercise>
</note>

</note>
```

## Misc

### Video

For now we will NOT add os-embed to videos in Link to Learning. 

### Interactives

No interactives in AP Bio. 


## Teacher Content

Notes: 
 - Teacher content should be placed within the content that it is nearest. If it cannot be placed within that content, it should be placed just after the content.
 - Teacher content **must not** contain any solutions. Those will be placed in Exercises via the assessment import spreadsheet. The import spreadsheet can specify whether an answer should be available to students or just to teachers and that will become some sort of flag in Exercises, for when 'embargoing' is possible.

We will not use the classes on these for styling in web view/PDF for the moment, but we will eventually. 

Look at these with Alina.

### Container

```html
<note class=”os-teacher”>
  <label>Teacher Edition</label>
  …
</note>
```
###Special Classes within Teacher Content

####Teaching Tips
```html
<note class="ost-tips-teaching">
  <label>Teaching Tips</label>
  ...
</note>
```

####Background Information
```html
<note class="ost-background-info">
  <label>Background Information</label>
  ...
</note>
```

####Misconception Alert
```html 
<note class=”ost-misconception-alert”>
  <label>Misconception Alert</label>
  …
</note>
```

####Teacher Demonstration
```html 
<note class=”ost-demonstration”>
  <label>Teacher Demonstration</label>
  …
</note>
```

## Assessments

**Note:** The tutor-only assessments **must NOT** appear in the CNXML modules. 

Scientific Thinking questions **must** be input (full XML) in the AP Science Practices Connection. 

For ALL questions, DELETE the existing solution CNXML. 

For questions that do NOT change, KEEP the existing cnxml and  add the embed code. (CNX will remove the existing question and just show the question in exercises, so no need to worry about double display.) 

For existing questions that have been modified, DELETE the existing CNXML and add the embed code. 

For new questions, do NOT add the new CNXML markup. DO add the embed code.  

## End of Section Review 

None. 

## Assessments that may be collated

### Visual Connection Questions
```html
<section class="ost-reading-discard ost-chapter-review visual-exercise">
  <title>Visual Connection Questions</title>
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

###Review Questions
```html
<section class="ost-reading-discard ost-chapter-review multiple-choice">
  <title>Review Questions</title>
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

###Critical Thinking Questions
```html
<section class="ost-reading-discard ost-chapter-review free-response">
  <title>Critical Thinking Questions</title>
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

###AP Test Prep
```html
<section class="ost-feature ost-reading-discard ap-test-prep”>
  <title>Test Prep for AP® Courses</title>
  <exercise class="os-exercise">
    <problem>
      <para><link class="os-embed" url="..." /></para>
    </problem>
   </exercise>
  ...
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
  - `ost-get-exercise` (tells Tutor to look for an exercise and add to the end of the section)
- Misc
  - `os-teacher`
    - `ost-tips-teaching`
    - `ost-background-info`
    - `ost-misconception-alert`
    - `ost-demonstration`
  - `ost-reading-discard`
  - `ost-sciprac-activity` (activity within `ap-science-practices`)
  - `ost-sciprac-scithink` (activity within `ap-science-practices`)
  - `st-sciprac-lab` (activity within `ap-science-practices`)
  - `ost-standards-apbio`
  - `ost-standards-def` (and include ost-tag-* next to this tag)
  - `ost-standards-name`
  - `ost-standards-description`
  - `ost-learning-objective-def` (for PLO’s)
  - `ost-standards-discard` (for big idea/EU, EK, SP)
- no prefix: visual styling only

## Visual-only

- `ap-connection` : Connection for AP® Courses 
- `experiment` : Scientific Method Connection (existing class name from AP Bio template)
- `evolution` : Evolution Connection (existing class name from AP Bio template)
- `career` : Career Connection (existing class name from AP Bio template)
- `ap-science-practices` : Science Practice Connection for AP® Courses 
- `interactive` : Link to Learning (existing class name from AP Bio template)
- `visual` : Visual Connection (replacing Art Connection)
- `ap-everyday` : Everyday Connection for AP® Courses 
- `key-terms`
- `learning-objectives` : on the section describing the Program Learning Objectives (not currently used for styling but may be in future)
- Exercises **Note:** Tutor doesn't use the exercise types within the module content, but these do end up as tags on the exercises in Exercises and are used to set up HWs and Reading Review problems. 
  - Within the flow of content
    NONE
  - At the End of Section
    NONE
  - End of Section Collatable Assessments
    - `visual-exercise`
    - `multiple-choice` : chapter review questions (existing class name from AP Bio template)
    - `free-response` : critical thinking questions (existing class name from AP Bio template)
    - `ap-test-prep` : Test Prep for AP® Courses
- End of Section Collatable Features
    - `summary`
    - `glossary`(do we have a glossary?)
