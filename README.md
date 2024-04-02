# Flat-file-to-xml-file---using-PERL-


write PERL script to convert flat file into XML that can be ingested into custom algorithm.


#!/usr/bin/perl

use strict;
use warnings;

# Open the flat file for reading
open my $fh, '<', 'input_flat_file.txt' or die "Cannot open input_flat_file.txt: $!";

# Open the output XML file for writing
open my $xml_fh, '>', 'output_xml_file.xml' or die "Cannot open output_xml_file.xml: $!";

# Print XML header
print $xml_fh "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";

# Start root element
print $xml_fh "<data>\n";

# Read each line of the flat file
while (my $line = <$fh>) {
    chomp $line;
    my @fields = split /\t/, $line; # Assuming tab-separated, change delimiter as needed

    # Start record element
    print $xml_fh "  <record>\n";

    # Iterate over fields and print as XML elements
    for my $i (0 .. $#fields) {
        my $field_name = "field$i"; # You can customize field names here
        print $xml_fh "    <$field_name>$fields[$i]</$field_name>\n";
    }

    # End record element
    print $xml_fh "  </record>\n";
}

# End root element
print $xml_fh "</data>\n";

# Close filehandles
close $fh;
close $xml_fh;

print "Conversion completed. XML file generated.\n";

