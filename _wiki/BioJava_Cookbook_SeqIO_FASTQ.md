---
title: BioJava:Cookbook:SeqIO:FASTQ
permalink: wiki/BioJava%3ACookbook%3ASeqIO%3AFASTQ
---

How do I work with nextgen sequencing reads in FASTQ format?
------------------------------------------------------------

The org.biojava.bio.program.fastq package provides support for reading
and writing nextgen sequencing reads in FASTQ format (FastqReader and
FastqWriter, respectively) and for converting FASTQ sequences into
proper biojava Sequences for analysis purposes (FastqTools).

The following code snippets demonstrate how to use the APIs for common
use cases.

### Convert between FASTQ variants

```java FastqReader fastqReader = new IlluminaFastqReader(); FastqWriter
fastqWriter = new SangerFastqWriter(); fastqWriter.write(new
File("sanger.fastq"), fastqReader.read(new File("illumina.fastq")));
```

### Convert only long sequences

```java FastqReader fastqReader = new IlluminaFastqReader(); FastqWriter
fastqWriter = new SangerFastqWriter(); FileWriter fileWriter = new
FileWriter(new File("sanger.fastq"))));

for (Fastq fastq : fastqReader.read(new File("illumina.fastq"))) {

` if (fastq.getSequence().length() > 16)`  
` {`  
`   fastqWriter.append(fileWriter, fastq);`  
` }`

} ```

### Convert between FASTQ variants using streaming API

```java FastqReader fastqReader = new IlluminaFastqReader();
IlluminaInputSupplier inputSupplier = Files.newReaderSupplier(new
File("illumina.fastq")); final FastqWriter fastqWriter = new
SangerFastqWriter(); final FileWriter fileWriter = new FileWriter(new
File("sanger.fastq"))));

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     fastqWriter.append(fileWriter, fastq);`  
`   }`  
` });`

```

### Convert only long sequences using streaming API

```java IlluminaFastqReader fastqReader = new IlluminaFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("illumina.fastq")); FastqWriter fastqWriter = new
SangerFastqWriter(); FileWriter fileWriter = new FileWriter(new
File("sanger.fastq"))));

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     if (fastq.getSequence().length() > 16)`  
`     {`  
`       fastqWriter.append(fileWriter, fastq);`  
`     }`  
`   }`  
` });`

```

### Count sequences

```java FastqReader fastqReader = new IlluminaFastqReader();

int count = 0; for (Fastq fastq : fastqReader.read(new
File("illumina.fastq"))) {

` count++:`

} System.out.println(count); ```

### Count sequences using streaming API

```java IlluminaFastqReader fastqReader = new IlluminaFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("illumina.fastq"));

final AtomicInteger count = new AtomicInteger();
fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     count.incrementAndGet();`  
`   }`  
` });`

System.out.println(count.get()); ```

### Count sequences using low-level API

```java IlluminaFastqReader fastqReader = new IlluminaFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("illumina.fastq"));

final AtomicInteger count = new AtomicInteger();
fastqReader.parse(inputSupplier, new ParseAdapter()

` {`  
`   @Override`  
`   public void complete() throws IOException`  
`   {`  
`     count.incrementAndGet();`  
`   }`  
` });`

System.out.println(count.get()); ```

### Pattern match description lines using low-level API

```java final Pattern pattern = Pattern.compile("^HWUSI-EAS100R:.\*$");
IlluminaFastqReader fastqReader = new IlluminaFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("illumina.fastq"));

fastqReader.parse(inputSupplier, new ParseAdapter()

` {`  
`   @Override`  
`   public void description(final String description) throws IOException`  
`   {`  
`     if (pattern.matches(description))`  
`     {`  
`       System.out.println(description);`  
`     }`  
`   }`  
` });`

```

### Create Sequences from FASTQ sequences

```java FastqReader fastqReader = new SangerFastqReader(); List<Sequence>
sequences = new LinkedList<Sequence>();

for (Fastq fastq : fastqReader.read(new File("sanger.fastq"))) {

` sequences.add(FastqTools.createSequence(fastq));`

} ```

### Create Sequences with streaming API

```java SangerFastqReader fastqReader = new SangerFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("sanger.fastq")); List<Sequence> sequences = new
LinkedList<Sequence>();

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     sequences.add(FastqTools.createSequence(fastq));`  
`   }`  
` });`

```

### Create PhredSequences ([DNAxInteger] symbols) from FASTQ sequences

```java FastqReader fastqReader = new SangerFastqReader();
List<PhredSequence> sequences = new LinkedList<PhredSequence>();

for (Fastq fastq : fastqReader.read(new File("sanger.fastq"))) {

` phredSequences.add(FastqTools.createPhredSequence(fastq));`

} ```

### Create PhredSequences ([DNAxInteger] symbols) using streaming API

```java SangerFastqReader fastqReader = new SangerFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("sanger.fastq")); List<PhredSequence> sequences = new
LinkedList<PhredSequence>();

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     sequences.add(FastqTools.createPhredSequence(fastq));`  
`   }`  
` });`

```

### Calculate mean p scores using streaming API

```java SangerFastqReader fastqReader = new SangerFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("sanger.fastq")); SummaryStatistics stats = new
SummaryStatistics(); StringBuilder sb = new StringBuilder(512);

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     stats.clear();`  
`     for (Double errorProbability : FastqTools.errorProbabilities(fastq))`  
`     {`  
`       stats.addValue(errorProbability);`  
`     }`  
`     sb.delete(0, sb.length());`  
`     sb.append(fastq.getDescription());`  
`     sb.append("\t");`  
`     sb.append(stats.getMean());`  
`     sb.append("\t");`  
`     sb.append(stats.getStandardDeviation());`  
`     System.out.println(sb.toString());`  
`   }`  
` });`

```

### Calculate mean p scores using streaming API and double array

```java SangerFastqReader fastqReader = new SangerFastqReader();
InputSupplier inputSupplier = Files.newReaderSupplier(new
File("sanger.fastq")); SummaryStatistics stats = new
SummaryStatistics(); StringBuilder sb = new StringBuilder(512);

fastqReader.stream(inputSupplier, new StreamListener()

` {`  
`   @Override`  
`   public void fastq(final Fastq fastq)`  
`   {`  
`     stats.clear();`  
`     int size = fastq.getSequence().length();`  
`     double[] errorProbabilities = FastqTools.errorProbabilties(fastq, new double[size]);`  
`     for (int i = 0; i < size; i++)`  
`     {`  
`       stats.addValue(errorProbabilities[i]);`  
`     }`  
`     sb.delete(0, sb.length());`  
`     sb.append(fastq.getDescription());`  
`     sb.append("\t");`  
`     sb.append(stats.getMean());`  
`     sb.append("\t");`  
`     sb.append(stats.getStandardDeviation());`  
`     System.out.println(sb.toString());`  
`   }`  
` });`

```
