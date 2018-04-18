## DESCRIPTION OF DATA ORGANIZATION AND METADATA IN THE LEGUME FEDERATION PRIMARY REPOSITORY AND FEDERATION SITES

Steven Cannon
Revision: 2017-01-09


Return to the <a href=".">metadata folder</a>.


### OBJECTIVES AND PRINCIPLES
1. A clear system (for curators and users)
  - Consistent, prescribed prefixes, abbreviations, etc.
2. Easy navigation for users
  - Limited directory depth (generally, only two directories deep)
  - Organization by species, then by genotype and data/analysis type
3. Borrow naming schemes from NCBI and Phytozome (but adapt in some places for clarity or 
    for other file types). Examples of similarities and differences:
  - NCBI doesn't maintain _primaryTranscript.fa files. Adopt this convention from Phytozome.
  - NCBI uses a _genomic.fna suffix for genome assembly (as well as a fairly complex directory 
    hierarchy for assembly components and tiling path, etc.). We will use a hybrid naming 
    system, with _pchr.fa for pseudochromosomes and _scaf.fa for scaffolds.
  - Phytozome annotation names are versioned only per the assembly name, which doesn't 
    allow for the possibility of multiple annotation versions on an assembly.
4. In cases where there are multiple analyses (assembly, then annotation), be explicit 
   about naming the type of analysis, and the analysis version. This could be done using 
   "assembly" and "annotation", but assembly could refer to transcriptome or genomic 
   assemblies, and "assembly" and "annotation" are also lengthy. So, shorten to "e.g. 
   "annot" in some cases. For other analysis types (synteny, diversity, etc.), also 
   specify abbreviations that are unambiguous but short.
5. Provenance is important. Retain the original README for data coming from other 
   repositories, and provide a structured README for this project - with same key name as 
   for the described files. Note the source repository clearly in the keyed project README. 
   Also record changed filenames (original and new), in the new README.


### PROCEDURE FOR MAKING A DATA REPOSITORY AT A FEDERATION SITE
In this case, the federation site is legumeinfo.org (and legumefederation.org, 
peanutbase.org, soybase.org). Similar procedures may be used for other federation sites, but 
the paths used in the protocol here will be different. Some naming conventions will also
inevitably differ - but as long as the conventions are consistent and transparent at each 
site, mappings or translations should be possible.

The basic, simple concepts of federated repositories are:
  - There are repositories (filesystems, with ftp and/or http access) at member LegFed sites
  - A set of standards or practices for directory and file naming facilitates sharing of 
    file resources among projects and repositories, where appropriate. For example, 
    Cool Season Food Legume and LegumeInfo may both benefit from holding the reference 
    chickpea genome assemblies and annotations - particularly if each projects makes changes
    to any files for chickpea (e.g. GFFs for display in browsers) - and wants to provide those
    files to users, for the purpose of reproducibility, transparency, and convenience.
  - Any modifications of files vs. original forms in a primary repository should be noted in
    a way that can be reproduced. 
  - Modified files or directories should be flagged in the file names, so that two files or 
    directories held at different repositories don't end up with the same names but different contents.
  - File or resource provenance, provenance, restrictions on use, etc., should be clearly noted.
  - Metadata should be stored in a way that makes it easy for people to keep the metadata with
    the files that the metadata describes.
  - Given the practices above (metadata records provenance, and stays with described files or projects,
    and modifications are noted, and modified files get unique names), files or directories can be
    re-hosted when appropriate - for example, at a data repository at CyVerse AND at LegumeInfo or
    CoolSeasonFoodLegume.
  - The primary level of granularity of metadata is a directory, containing files that are related in
    some meaningful biological way: a directory with a genome assembly and the associated metadata; 
    a set of annotations for a genome assembly, and the associated metadata, etc. 
    Each such directory is keyed with a unique four-letter key name (as part of the directory name), 
    and the metadata files contained within the directory contains the same key as the directory.
  - The keyed directories are typically organized within a human-readable containing directory,
    which is named by project convention. The top-level directory is typically named by
    genus and species, e.g. `Medicago_truncatula` or `Glycine_max`
  - Directories within species directories directories should typically contain:
      - broad data type (e.g. "genome" or "transcriptome")
      - accession (e.g. `A17_HM341` or MilvusB
      - a version (e.g. v2.1 or v2)



Notes below describe procedures specifically at the data filesystem associated with legumeinfo.
Presumably, similar practices would be used for other "federation member" repositories.

Data is initially populated and managed at legumeinfo - though might similarly 
initially be managed at another repository.

Data are organized by species (or major cross-cutting data type such as "gene_families", 
in directories at /usr/local/www/data/, in either public/ or private/. 
These directories are accessed at lis-stage.agron.iastate.edu, and are  
mounted in production at legumeinfo.org at the same directory address, and are accessible
via browser at http://lis-stage.agron.iastate.edu/data/ or http://legumeinfo.org/data/.

Data for this data directory will typically come from another repository, sometimes via 
a local data repository. For LIS development at Ames, this repository is maintained at the
machines "cicer" and "cicer" -- where the /data directory is mounted from the  NAS "mora".

The primary purpose for the repository is to expose data sets that are used at LIS or the other
respective genomic data portals (GDPs). To that end, not every piece of genomic data for
a species needs to be housed in the repository. (There may be some instances, though, where
extensive, multifaceted data sets are held for some species).


### DIRECTORY STRUCTURE AND NAMING

  Genus_species/GENOTYPE.ANALYSIS#/   or 
  Genus_species/GENOTYPE.ANALYSIS#.ANALYSIS#/ (for e.g. genome assembly, annotation)
    GENSP is a five-letter abbreviation of the GENus and SPecies, lower case,
      e.g. glyma for Glycine max or medtr for Medicago truncatula
    GENOTYPE is genotype name
    ANALYSIS# is e.g. "gnm2" for a genome assembly 2.0)
    where analysis_type is abbreviated (generally by removing vowels and truncating):
      ann => annotation
      gnm => genome assembly
      tcp => transcriptome
      syn => synteny
      div => diversity
      gws == GWAS 
    In the version (v#.#), v1 implies v1.0. The decimal is used for subversions, e.g. v1.1

  Examples of directory names for a species:
    Lupinus_angustifolius/
      Tanjil.gnm1/
      Tanjil.gnm1.ann1/
      Tanjil.gnm1.syn1/
      Tanjil.tcp1/
      Unicrop.tcp1/
  
### README FILES:
  Retain the original README file(s) from the original repository, if any. Prefix
  such files with "original_readme.", followed by the repository name and ".txt"
  
  Also provide a template-based, structured README, with filename with the form
  README.KEY#.md


### FILE NAMING SCHEME
  
Principles in the file naming are:
    - Include brief, prescribed, descriptive prefixes, including
      - gensp, e.g. glyma
      - analysis type and version, e.g. gnm1 or tcp1
      - key#, e.g. DFgp  
                   DFgp   DFgp  DFgp
      - suffix, giving molecule type, e.g. gene.gff3 or protein.faa

Within the GENOTYPE.ANALYSIS#/ directories, files have this format:
gensp.GENOTYPE.ANALYSIS#.KEY#.file_type.ext.gz
where file_type is a prescribed, abbreviated description of the contents, 
and where KEY# is a four-letter character string, uniquely identifying a file
or files referred to by the README file containing the same key.
Examples of file_type abbreviations (these generally follow Phytozome and GenBank patterns,
but with some exceptions - for example, GenBank doesn't have _primaryTranscript forms, and
neither subdivides GFF files into subtypes as needed in legumeinfo and peanutbase for 
database loading and browsers):

  Annotation files:
    .KEY#.annot.ahrd.txt.gz
    .KEY#.cds.fna.gz
    .KEY#.cds_primaryTranscript.fna.gz
    .KEY#.gene.gff3.gz
    .KEY#.gene_for_chado.gff3.gz  -- in cases where this specialized file has been generated
    .KEY#.gene_for_gbrowse.gff3.gz  -- in cases where this specialized file has been generated
    .KEY#.protein.faa.gz
    .KEY#.protein_primaryTranscript.faa.gz
  Genome assembly files:
    .KEY#.pchr.fna.gz   -- Pseudomolecule assemblies
    .KEY#.pchr_plus_scaff_ge10k.fna.gz  -- Pseudomolecule assemblies plus larger scaffolds. 
                                          This may vary.
    .KEY#.pchr_plus_unanchored.fna.gz  -- Pseudomolecule assemblies plus scaffolds. 
                                          This may vary.
    .KEY#.scaf.fna.gz  -- All scaffolds
    .KEY#.scaffs_unassigned.fna.gz  -- Unplaced scaffolds
  Transcriptome assembly files:
    .KEY#.METHOD.fna.gz -- e.g. .ycvS.Trinity.ffn
  README files
    README.origin.REPOSITORY.txt 
    README.GENSP.KEY#.md  -- template-based README file for this repository, in markdown format


### EXAMPLES OF DIRECTORIES AND FILES:
  
### GENOME ASSEMBLY

  Lupinus_angustifolius/
    Tanjil.gnm1/
      README.Qq0N.md
      lupan.Tanjil.gnm1.Qq0Na.pchr.fna.gz
      lupan.Tanjil.gnm1.Qq0Nc.scaf.fna.gz
      lupan.Tanjil.gnm1.Qq0Nd.scaf_unassigned.fna.gz
      original_readme.lupinexpress.txt

  Trifolium_pratense/
    MilvusB.gnm2.1/
      README.gNmT.md
      tripr.MilvusB.gnm2.1.gNmTa.pchr_plus_unanchored.fna.gz

  Vigna_angularis/
    Gyeongwon.genome3/
      README.JyYC.md
      vigan.Gyeongwon.genome1.JyYC.pchr_plus_unanchored.fna.gz


### GENOME ANNOTATION

  Lupinus_angustifolius/
    Tanjil.gnm1.ann1/
      README.nnV9.md
      lupan.Tanjil.gnm1.ann1.nnV9.cds.fna.gz
      lupan.Tanjil.gnm1.ann1.nnV9.protein.fna.gz
      original_readme.lupinexpress.txt

  Trifolium_pratense/
    MilvusB.gnm2.1.ann1/
      README.DFgp.md
      tripr.MilvusB.genome2.1.annot1.DFgp.annot.ahrd.txt.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.cds.fna.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.cds_primaryTranscript.fna.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.gene_for_chado.gff.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.gene_for_gbrowse.gff.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.protein.faa.gz
      tripr.MilvusB.genome2.1.annot1.DFgp.protein_primaryTranscript.faa.gz

  Vigna_angularis/
    vigan.Gyeongwon.genome3.annot1/
      README.3Nz5.md
      vigan.Gyeongwon.genome3.annot1.3Nz5.annot.ahrd.txt.gz
      vigan.Gyeongwon.genome3.annot1.3Nz5.cds.fna.gz
      vigan.Gyeongwon.genome3.annot1.3Nz5.cds_primaryTranscript.fna.gz
      vigan.Gyeongwon.genome3.annot1.3Nz5.gene.gff.gz
      vigan.Gyeongwon.genome3.annot1.3Nz5.protein.faa.gz
      vigan.Gyeongwon.genome3.annot1.3Nz5.protein_primaryTranscript.faa.gz

### TRANSCRIPTOME ASSEMBLY

  Lupinus_angustifolius/
    P27255.tcp1/
      README.ycvS.md
      lupan.P27255.tcpt1.ycvS.Trinity.fna.gz
      original_readme.lupinexpress.txt

    Tanjil.tcp1/
      README.p27w.md
      lupan.Tanjil.tcpt1.p27w.Trinity.fna.gz
      original_readme.lupinexpress.txt
      reads

    Unicrop.tcp1/
      README.YVT4.md
      lupan.Unicrop.tcpt1.YVT4.Trinity.fna.gz
      original_readme.lupinexpress.txt
