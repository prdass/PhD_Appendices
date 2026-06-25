#!/bin/bash
ALIGN_DIR="PRD_ONT/neurons/outputs/align"
OUTPUT_DIR="${ALIGN_DIR}/primary"
mkdir -p "$OUTPUT_DIR"

echo "Filtering for primary alignments in: $ALIGN_DIR"
echo "Output will be saved to: $OUTPUT_DIR"

for bamfile in ${ALIGN_DIR}/*.sorted.bam; do
    sample=$(basename "$bamfile" .sorted.bam)
    echo "Processing $sample..."
    samtools view -@ 8 -b -F 0x100 "$bamfile" > "${OUTPUT_DIR}/${sample}.primary.bam"
    samtools view -@ 8 -b -F 0x400 "${OUTPUT_DIR}/${sample}.primary.bam" > "${OUTPUT_DIR}/${sample}.primary.nodup.bam"
    samtools sort -@ 8 -o "${OUTPUT_DIR}/${sample}.primary.sorted.bam" "${OUTPUT_DIR}/${sample}.primary.nodup.bam"
    samtools index "${OUTPUT_DIR}/${sample}.primary.sorted.bam"
    rm "${OUTPUT_DIR}/${sample}.primary.bam" "${OUTPUT_DIR}/${sample}.primary.nodup.bam"
    echo "$sample: Primary, non-duplicate, sorted and indexed"
    echo ""
done
