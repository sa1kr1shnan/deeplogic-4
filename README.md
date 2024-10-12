Part 4: Template Optimization and Efficiency
Approach:

Generalized extraction rules to handle multiple formats.
Implemented efficiency optimizations to improve performance.
Added comments explaining generalizations and optimizations.

Challenges:

Balancing flexibility with performance.
Handling diverse document structures efficiently.

Solution:

Compiled frequently used regex patterns for improved performance.
Implemented a single-pass extraction function to reduce redundant processing.
Used more flexible patterns to handle variations in field names and formats.

Key Code Section:

CURRENCY_REGEX = re.compile(r'\$?\s*\d+(?:,\d{3})*(?:\.\d{2})?')
DATE_REGEX = re.compile(r'\d{1,2}[-./ ]\w+[-./ ]\d{2,4}')

# Optimization 2: Use a single pass extraction for efficiency
def extract_invoice_data(document_text):
    extracted_data = {}
    lines = document_text.split('\n')
    
    for line in lines:
        # Extract multiple pieces of information in a single pass
        if not extracted_data.get('Invoice Number'):
            invoice_num = re.search(r'(?:Invoice|Bill)\s*(?:No|Number|#)[:.]?\s*(\S+)', line)
            if invoice_num:
                extracted_data['Invoice Number'] = invoice_num.group(1)
        
